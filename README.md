# django_cve_2019_19844_poc
PoC for [CVE-2019-19844](https://www.djangoproject.com/weblog/2019/dec/18/security-releases/)

![](https://github.com/andripwn/django_cve201919844/badge.svg)

# Requirements

- Python 3.7.x
- PostgreSQL 9.5 or higher

## Setup

1. Create database(e.g. `django_cve_2019_19844_poc`)
1. Set the database name to the environment variable `DJANGO_DATABASE_NAME`(e.g. `export DJANGO_DATABASE_NAME=django_cve_2019_19844_poc`)
1. Run `pip install -r requirements.txt && ./manage.py migrate --noinput`
1. Create the following user with `shell` command:

```python
>>> from django.contrib.auth import get_user_model
>>> User = get_user_model()
>>> User.objects.create_user('mike123', 'mike@example.org', 'test123')
```

## Procedure For Reproducing

1. Run `./manage.py runserver`
1. Open `http://127.0.0.1:8000/accounts/password-reset/`
1. Input `mıke@example.org` (Attacker's email), and click send button
1. Receive email (Check console), and reset password
1. Login as `mike123` user

![Email](/images/email.jpg "Email")
