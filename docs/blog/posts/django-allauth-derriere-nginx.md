---
date:
  created: 2026-06-16

---

# Django allauth derrière Nginx : résoudre le 403 et l'erreur SMTP en production

## Introduction
Lors du déploiement d'un projet Django utilisant **django-allauth** sur un VPS avec **Nginx + Gunicorn**, j'ai rencontré deux problèmes bloquants sur la page d'inscription :

1. Une erreur **403 Forbidden** au moment du POST du formulaire.
2. Une erreur **SMTPAuthenticationError (535)** empêchant l'envoi de l'email de vérification via **AWS SES**.

Cet article détaille le diagnostic complet et les solutions appliquées.

<!-- more -->

## Environnement technique

- **Python** 3.13
- **Django** 6.0
- **django-allauth** (dernière version)
- **Gunicorn** 26.0
- **Nginx** sur Ubuntu 24.04 LTS (OVH VPS)
- **AWS SES** pour l'envoi d'emails
- Authentification par email uniquement (sans username)

## Problème 1 — 403 Forbidden sur le formulaire d'inscription

### Symptôme

Le formulaire d'inscription s'affiche correctement (GET → 200), mais la soumission renvoie systématiquement un **403 Forbidden** sans message d'erreur explicite dans le navigateur.

### Diagnostic

La première réflexe est de vérifier les logs Nginx :

```bash
sudo tail -20 /var/log/nginx/error.log
```

Rien de suspect côté Nginx. On surveille alors les logs Gunicorn en temps réel pendant la soumission du formulaire :

```bash
sudo journalctl -u gunicorn -f
```

Et là, l'erreur réelle apparaît :

```
django.core.exceptions.PermissionDenied: Unable to determine client IP address
  File "allauth/account/adapter.py", line 848, in get_client_ip
    raise PermissionDenied("Unable to determine client IP address")
```

**Ce n'est pas un problème CSRF** — c'est le système de **rate limiting d'allauth** qui échoue. Allauth essaie de récupérer l'adresse IP du client pour limiter les tentatives d'inscription, mais derrière un proxy Nginx, l'IP n'est pas directement disponible dans `REMOTE_ADDR` : elle est transmise via le header `X-Forwarded-For`.

### Vérifications préalables (pistes éliminées)

Avant de trouver la vraie cause, plusieurs pistes ont été vérifiées :

**Vérifier que le token CSRF est bien dans le HTML :**
```bash
curl -k https://monsite.com/accounts/signup/ | grep csrfmiddlewaretoken
```

**Tester un POST complet avec curl :**
```bash
# Récupérer le cookie CSRF
curl -k -c /tmp/cookies.txt https://monsite.com/accounts/signup/ > /dev/null

# Soumettre le POST
curl -k -b /tmp/cookies.txt -X POST https://monsite.com/accounts/signup/ \
  -H "Referer: https://monsite.com/accounts/signup/" \
  -d "csrfmiddlewaretoken=VALEUR_DU_TOKEN" \
  -v 2>&1 | grep "< HTTP"
```

**Vérifier la configuration CSRF dans settings.py :**
```python
CSRF_TRUSTED_ORIGINS = ['https://monsite.com', 'https://www.monsite.com']
SECURE_PROXY_SSL_HEADER = ('HTTP_X_FORWARDED_PROTO', 'https')
```

**Vérifier la config Nginx :**
```nginx
location / {
    include proxy_params;
    proxy_pass http://unix:/var/www/monprojet/gunicorn.sock;
    proxy_set_header X-Forwarded-Proto $scheme;
}
```

> Ne pas dupliquer `proxy_pass` — Nginx retourne une erreur de configuration au test (`nginx -t`).

### Solution — CustomAccountAdapter

La solution est de surcharger la méthode `get_client_ip()` de l'adapteur allauth pour lire correctement le header `X-Forwarded-For` transmis par Nginx.

**Créer `accounts/adapter.py` :**

```python
from allauth.account.adapter import DefaultAccountAdapter
from django.http import HttpRequest

class CustomAccountAdapter(DefaultAccountAdapter):
    def get_client_ip(self, request: HttpRequest):
        """
        Récupère l'IP client derrière un proxy Nginx.
        Nginx transmet l'IP réelle via le header HTTP_X_FORWARDED_FOR.
        En l'absence de ce header, on utilise REMOTE_ADDR.
        """
        x_forwarded_for = request.META.get('HTTP_X_FORWARDED_FOR')
        if x_forwarded_for:
            return x_forwarded_for.split(',')[0].strip()
        return request.META.get('REMOTE_ADDR', '127.0.0.1')
```

**Déclarer l'adapter dans `settings.py` :**

```python
ACCOUNT_ADAPTER = 'accounts.adapter.CustomAccountAdapter'
```

**Redémarrer Gunicorn :**

```bash
sudo systemctl restart gunicorn
```

Le formulaire d'inscription fonctionne désormais correctement.

## Problème 2 — SMTPAuthenticationError (535) avec AWS SES

### Symptôme

Après résolution du 403, l'inscription déclenche maintenant l'envoi de l'email de vérification — mais une nouvelle erreur apparaît :

```
SMTPAuthenticationError at /accounts/signup/
(535, b'Authentication Credentials Invalid')
```

### Diagnostic

Vérifier ce que Django lit réellement depuis les variables d'environnement :

```python
# Dans le shell Django
python manage.py shell

from django.conf import settings
print(repr(settings.EMAIL_HOST_USER))
print(repr(settings.EMAIL_HOST_PASSWORD))
print(settings.EMAIL_HOST)
```

Tester l'envoi en passant les credentials directement, sans passer par le `.env` :

```python
from django.core.mail import get_connection, send_mail

connection = get_connection(
    backend='django.core.mail.backends.smtp.EmailBackend',
    host='email-smtp.eu-west-3.amazonaws.com',
    port=587,
    username='SMTP_USER',
    password='SMTP_PASSWORD',
    use_tls=True,
)

send_mail(
    subject='Test SES',
    message='Test',
    from_email='noreply@monsite.com',
    recipient_list=['mon_email@gmail.com'],
    connection=connection,
)
```

> Si l'envoi fonctionne avec les credentials en dur mais pas via le `.env`, le problème vient du fichier `.env`.

### Cause

Un **espace parasite** avait été introduit lors du copier-coller du mot de passe SMTP dans le fichier `.env`.

### Solution

Corriger le `.env` en vérifiant l'absence d'espaces ou de retours à la ligne :

```bash
nano /var/www/monprojet/.env
```

```
SES_SMTP_USER=AKIAXXXXXXXXXXXXXXXX
SES_SMTP_PASSWORD=XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
```

> Le mot de passe SMTP SES fait exactement **44 caractères**. S'il est plus court, il est tronqué ou mal copié.

**Redémarrer Gunicorn pour recharger les variables d'environnement :**

```bash
sudo systemctl restart gunicorn
```

L'email de vérification est envoyé correctement.

## Configuration AWS SES (rappel)

Les credentials SMTP SES ne sont **pas** les clés IAM classiques. Ils sont générés spécifiquement depuis :

**AWS Console → SES → SMTP settings → Create SMTP credentials**

La configuration dans `settings.py` :

```python
if env('DJANGO_DEVELOPMENT') == 'True':
    EMAIL_BACKEND = "django.core.mail.backends.console.EmailBackend"
else:
    EMAIL_BACKEND = "django.core.mail.backends.smtp.EmailBackend"
    EMAIL_HOST = "email-smtp.eu-west-3.amazonaws.com"  # adapter selon ta région
    EMAIL_PORT = 587
    EMAIL_USE_TLS = True
    EMAIL_HOST_USER = env("SES_SMTP_USER")
    EMAIL_HOST_PASSWORD = env("SES_SMTP_PASSWORD")

DEFAULT_FROM_EMAIL = "Mon Site <noreply@monsite.com>"
SERVER_EMAIL = "noreply@monsite.com"
```

## Récapitulatif

| Problème | Symptôme | Cause réelle | Solution |
|---|---|---|---|
| 403 sur POST signup | Formulaire refusé silencieusement | allauth ne peut pas déterminer l'IP derrière Nginx | `CustomAccountAdapter.get_client_ip()` |
| SMTPAuthenticationError 535 | Email de vérification non envoyé | Espace parasite dans le `.env` | Corriger les credentials SES |

## Commandes utiles pour le diagnostic

```bash
# Voir les logs Gunicorn en temps réel
sudo journalctl -u gunicorn -f

# Voir les 50 dernières lignes des logs Gunicorn
sudo journalctl -u gunicorn -n 50 --no-pager

# Voir les logs Nginx
sudo tail -20 /var/log/nginx/error.log

# Tester la config Nginx avant redémarrage
sudo nginx -t

# Redémarrer les services
sudo systemctl restart nginx
sudo systemctl restart gunicorn

# Lister les services gunicorn actifs
sudo systemctl list-units | grep gunicorn
```

## En résumé

Ces deux problèmes sont fréquents lors du déploiement de django-allauth en production derrière un proxy Nginx. Le point clé à retenir : **un 403 sur un formulaire allauth n'est pas forcément un problème CSRF** — les logs Gunicorn sont essentiels pour trouver la vraie cause. Et pour les credentials SMTP, toujours vérifier l'absence de caractères parasites dans le `.env`.