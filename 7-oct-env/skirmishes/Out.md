Displaying: ./manage.py
#!/usr/bin/env python
"""Django's command-line utility for administrative tasks."""
import os
import sys


def main():
    """Run administrative tasks."""
    os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'skirmishes.settings')
    try:
        from django.core.management import execute_from_command_line
    except ImportError as exc:
        raise ImportError(
            "Couldn't import Django. Are you sure it's installed and "
            "available on your PYTHONPATH environment variable? Did you "
            "forget to activate a virtual environment?"
        ) from exc
    execute_from_command_line(sys.argv)


if __name__ == '__main__':
    main()

-------------------------------

Displaying: ./Ohaio/admin.py
from django.contrib import admin

# Register your models here.

-------------------------------

Displaying: ./Ohaio/apps.py
from django.apps import AppConfig


class OhaioConfig(AppConfig):
    default_auto_field = 'django.db.models.BigAutoField'
    name = 'Ohaio'

-------------------------------

Displaying: ./Ohaio/migrations/__init__.py

-------------------------------

Displaying: ./Ohaio/models.py
from django.db import models

# Create your models here.

-------------------------------

Displaying: ./Ohaio/tests.py
from django.test import TestCase

# Create your tests here.

-------------------------------

Displaying: ./Ohaio/url.py
from django.urls import path
from . import views

urlpatterns = [
    path("", views.index, name="index"),  # Corrected from "/" to ""
    path("trash", views.index1, name="index1"),
    path("<str:name>", views.great, name="great"),
    path("<str:name>/<int:number>", views.useless, name="useless")
]
-------------------------------

Displaying: ./Ohaio/views.py
from django.http import HttpResponse
from django.shortcuts import render

# Create your views here.
str = ''' <h1>Lorem ipsum dolor sit amet consectetur, adipisicing elit. Necessitatibus
alias odio, id, voluptas accusantium eos vero labore cumque nihil quod ipsa et omnis
voluptatem accusamus tenetur consequatur deserunt quas in.</h1>'''
def index(request):
    return render(request, "index.html")
def index1(request):
    return HttpResponse(str)
def great(request, name):
    return HttpResponse( f"<h1> Hello , {name} </h1> {request.__dict__}")
def useless(request, text, number):
    return render(request, "useless.html",{
        "text":text, "number":number
    })
-------------------------------

Displaying: ./Ohaio/__init__.py

-------------------------------

Displaying: ./skirmishes/asgi.py
"""
ASGI config for skirmishes project.

It exposes the ASGI callable as a module-level variable named ``application``.

For more information on this file, see
https://docs.djangoproject.com/en/4.2/howto/deployment/asgi/
"""

import os

from django.core.asgi import get_asgi_application

os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'skirmishes.settings')

application = get_asgi_application()

-------------------------------

Displaying: ./skirmishes/settings.py
"""
Django settings for skirmishes project.

Generated by 'django-admin startproject' using Django 4.2.10.

For more information on this file, see
https://docs.djangoproject.com/en/4.2/topics/settings/

For the full list of settings and their values, see
https://docs.djangoproject.com/en/4.2/ref/settings/
"""

from pathlib import Path

# Build paths inside the project like this: BASE_DIR / 'subdir'.
BASE_DIR = Path(__file__).resolve().parent.parent


# Quick-start development settings - unsuitable for production
# See https://docs.djangoproject.com/en/4.2/howto/deployment/checklist/

# SECURITY WARNING: keep the secret key used in production secret!
SECRET_KEY = 'django-insecure-*sn#90q-uv-yk9!i+7f9484jf62+d6#=w8n$%tt8u614i15qle'

# SECURITY WARNING: don't run with debug turned on in production!
DEBUG = True

ALLOWED_HOSTS = []


# Application definition

INSTALLED_APPS = [
    'Ohaio',
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
]

MIDDLEWARE = [
    'django.middleware.security.SecurityMiddleware',
    'django.contrib.sessions.middleware.SessionMiddleware',
    'django.middleware.common.CommonMiddleware',
    'django.middleware.csrf.CsrfViewMiddleware',
    'django.contrib.auth.middleware.AuthenticationMiddleware',
    'django.contrib.messages.middleware.MessageMiddleware',
    'django.middleware.clickjacking.XFrameOptionsMiddleware',
]

ROOT_URLCONF = 'skirmishes.urls'

TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]

WSGI_APPLICATION = 'skirmishes.wsgi.application'


# Database
# https://docs.djangoproject.com/en/4.2/ref/settings/#databases

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': BASE_DIR / 'db.sqlite3',
    }
}


# Password validation
# https://docs.djangoproject.com/en/4.2/ref/settings/#auth-password-validators

AUTH_PASSWORD_VALIDATORS = [
    {
        'NAME': 'django.contrib.auth.password_validation.UserAttributeSimilarityValidator',
    },
    {
        'NAME': 'django.contrib.auth.password_validation.MinimumLengthValidator',
    },
    {
        'NAME': 'django.contrib.auth.password_validation.CommonPasswordValidator',
    },
    {
        'NAME': 'django.contrib.auth.password_validation.NumericPasswordValidator',
    },
]


# Internationalization
# https://docs.djangoproject.com/en/4.2/topics/i18n/

LANGUAGE_CODE = 'en-us'

TIME_ZONE = 'UTC'

USE_I18N = True

USE_TZ = True


# Static files (CSS, JavaScript, Images)
# https://docs.djangoproject.com/en/4.2/howto/static-files/

STATIC_URL = 'static/'

# Default primary key field type
# https://docs.djangoproject.com/en/4.2/ref/settings/#default-auto-field

DEFAULT_AUTO_FIELD = 'django.db.models.BigAutoField'

-------------------------------

Displaying: ./skirmishes/urls.py
"""
URL configuration for skirmishes project.

The `urlpatterns` list routes URLs to views. For more information please see:
    https://docs.djangoproject.com/en/4.2/topics/http/urls/
Examples:
Function views
    1. Add an import:  from my_app import views
    2. Add a URL to urlpatterns:  path('', views.home, name='home')
Class-based views
    1. Add an import:  from other_app.views import Home
    2. Add a URL to urlpatterns:  path('', Home.as_view(), name='home')
Including another URLconf
    1. Import the include() function: from django.urls import include, path
    2. Add a URL to urlpatterns:  path('blog/', include('blog.urls'))
"""
from django.contrib import admin
from django.urls import( include,path)

urlpatterns = [
    path('admin/', admin.site.urls),
    path('Ohaio/', include("Ohaio.url"))
]

-------------------------------

Displaying: ./skirmishes/wsgi.py
"""
WSGI config for skirmishes project.

It exposes the WSGI callable as a module-level variable named ``application``.

For more information on this file, see
https://docs.djangoproject.com/en/4.2/howto/deployment/wsgi/
"""

import os

from django.core.wsgi import get_wsgi_application

os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'skirmishes.settings')

application = get_wsgi_application()

-------------------------------

Displaying: ./skirmishes/__init__.py

-------------------------------

