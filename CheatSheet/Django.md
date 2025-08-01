# Django Cheatsheet

## Install & Project Setup
pip install django  
django-admin startproject mysite  
cd mysite  
python manage.py runserver  
python manage.py startapp blog  
python manage.py makemigrations  
python manage.py migrate  
python manage.py createsuperuser  
python manage.py shell  
python manage.py collectstatic  

## Project Structure
mysite/  
├─ manage.py  
├─ mysite/  
│  ├─ settings.py  
│  ├─ urls.py  
│  └─ wsgi.py  
├─ blog/  
│  ├─ models.py  
│  ├─ views.py  
│  ├─ urls.py  
│  ├─ admin.py  
│  ├─ apps.py  
│  ├─ tests.py  

## Settings
DEBUG = True  
ALLOWED_HOSTS = ['*']  
INSTALLED_APPS = [ 'django.contrib.admin', 'blog', ]  
DATABASES = { 'default': { 'ENGINE': 'django.db.backends.sqlite3', 'NAME': BASE_DIR / 'db.sqlite3', } }  
STATIC_URL = '/static/'  
MEDIA_URL = '/media/'  
TIME_ZONE = 'UTC'  
LANGUAGE_CODE = 'en-us'  
SECRET_KEY = 'your_secret_key'  

## Models
from django.db import models  
class Post(models.Model):  
  title = models.CharField(max_length=200)  
  content = models.TextField()  
  published = models.DateTimeField(auto_now_add=True)  
  author = models.ForeignKey('auth.User', on_delete=models.CASCADE)  
  def __str__(self):  
    return self.title  

## Migrations
python manage.py makemigrations  
python manage.py migrate  

## Admin
from django.contrib import admin  
from .models import Post  
admin.site.register(Post)  

## Views
from django.shortcuts import render  
def home(request):  
  return render(request, 'home.html')  
from django.http import HttpResponse  
def hello(request):  
  return HttpResponse("Hello Django!")  

## Class-based Views
from django.views.generic import ListView  
class PostList(ListView):  
  model = Post  
  template_name = 'post_list.html'  

## Templates
{% extends 'base.html' %}  
{% block content %}  
  <h1>{{ post.title }}</h1>  
  <p>{{ post.content }}</p>  
{% endblock %}  
{{ variable }}  
{% for post in posts %} ... {% endfor %}  
{% if user.is_authenticated %} ... {% endif %}  
{% url 'home' %}  
{% static 'img/logo.png' %}  

## URLs
from django.urls import path  
from . import views  
urlpatterns = [  
  path('', views.home, name='home'),  
  path('post/<int:id>/', views.post_detail, name='post_detail'),  
]  
include('blog.urls')  

## Forms
from django import forms  
class PostForm(forms.ModelForm):  
  class Meta:  
    model = Post  
    fields = ['title', 'content']  

## Form Usage
form = PostForm(request.POST or None)  
if form.is_valid():  
  form.save()  

## Authentication
from django.contrib.auth import authenticate, login, logout  
user = authenticate(username='user', password='pass')  
login(request, user)  
logout(request)  

## Permissions
from django.contrib.auth.decorators import login_required  
@login_required  
def dashboard(request):  
  ...  

## Static Files
STATIC_URL = '/static/'  
STATICFILES_DIRS = [ BASE_DIR / 'static', ]  
{% load static %}  
<link rel="stylesheet" href="{% static 'css/style.css' %}">  

## Media Files
MEDIA_URL = '/media/'  
MEDIA_ROOT = BASE_DIR / 'media'  
<img src="{{ post.image.url }}">  

## QuerySet API
Post.objects.all()  
Post.objects.filter(author=request.user)  
Post.objects.get(id=1)  
Post.objects.order_by('-published')  
Post.objects.exclude(title='Draft')  
Post.objects.count()  
Post.objects.first()  
Post.objects.last()  

## Model Methods
def get_absolute_url(self):  
  return reverse('post_detail', args=[str(self.id)])  

## Reverse URL
from django.urls import reverse  
reverse('home')  

## Custom Management Command
from django.core.management.base import BaseCommand  
class Command(BaseCommand):  
  def handle(self, *args, **kwargs):  
    print("Custom command")  

## Signals
from django.db.models.signals import post_save  
from django.dispatch import receiver  
@receiver(post_save, sender=Post)  
def post_saved(sender, instance, **kwargs):  
  print('Post saved:', instance.title)  

## Pagination
from django.core.paginator import Paginator  
paginator = Paginator(posts, 10)  
page_obj = paginator.get_page(page_number)  

## Email
from django.core.mail import send_mail  
send_mail('Subject', 'Body', 'from@site.com', ['to@site.com'])  

## File Upload
class File(models.Model):  
  file = models.FileField(upload_to='uploads/')  

## REST API
pip install djangorestframework  
INSTALLED_APPS += ['rest_framework']  
from rest_framework import serializers, viewsets  
class PostSerializer(serializers.ModelSerializer):  
  class Meta: model = Post; fields = '__all__'  
class PostViewSet(viewsets.ModelViewSet):  
  queryset = Post.objects.all()  
  serializer_class = PostSerializer  

## DRF Routing
from rest_framework.routers import DefaultRouter  
router = DefaultRouter()  
router.register(r'posts', PostViewSet)  

## Testing
from django.test import TestCase  
class PostTest(TestCase):  
  def test_str(self):  
    post = Post(title='Test')  
    self.assertEqual(str(post), 'Test')  

## Shell
python manage.py shell  
from blog.models import Post  
Post.objects.all()  

## Fixtures
python manage.py dumpdata blog.Post  
python manage.py loaddata mydata.json  

## Internationalization
LANGUAGES = [('en', 'English'), ('uk', 'Ukrainian')]  
from django.utils.translation import gettext as _  
_("My text")  

## CSRF Token
{% csrf_token %}  

## Sessions
request.session['key'] = 'value'  
request.session.get('key')  

## Caching
from django.core.cache import cache  
cache.set('my_key', 'value', timeout=60)  
cache.get('my_key')  

## Logging
import logging  
logger = logging.getLogger(__name__)  
logger.info('Info message')  

## Custom Error Pages
handler404 = 'blog.views.page_not_found'  
handler500 = 'blog.views.server_error'  

## Deployment
python manage.py collectstatic  
gunicorn mysite.wsgi  
DEBUG = False  

## Best Practices
Use virtualenv  
Keep secret key safe  
Use DEBUG=False in production  
Validate user input  
Use migrations for DB changes  
Write unit tests  
Use prefetch/select_related for queries  
Keep models thin  
Use custom user model  
Limit admin access  
Document code  
Organize settings  
Split settings for dev/prod  
Use environment variables  
Limit file upload size  
Use pagination  
Cache expensive queries  
Monitor performance  
Audit security  
Sanitize data  
Handle errors gracefully  
Use signals sparingly  
Manage static/media files  
Automate deployment  
Use CI/CD  
Test migrations before deploy  
Review dependencies  
Update Django regularly  
Avoid raw SQL  
Use Django ORM  
Prefer class-based views for reuse  
Structure apps logically  
Document endpoints  
Limit session data  
Use templates for presentation  
Keep logic out of templates  
Use template tags/filters  
Support localization  
Lint code  
Keep changelog  
Refactor old code  
Archive unused apps  
Test edge cases  
Use .env files for secrets  
Use gunicorn/uwsgi for prod  
Enable HTTPS  
Set allowed hosts  
Minimize third-party packages  
Monitor error logs  
Automate backups  
Keep admin secure  
Test static files  
Comment complex logic  
Organize templates  
Use proper naming  
Prefer settings module  
Test with real data  
Limit global imports  
Support REST API  
Document models  
Use signals for audit/logging  
Keep migrations clean  
Automate tests  
Prefer DRF for APIs  
Handle file uploads securely  
Limit query size  
Support multi-language  
Use custom managers  
Test user flows  
Review admin permissions  
Use custom error pages  
Profile performance  
Monitor DB usage  
Backup DB regularly  
Document custom commands  
Automate management tasks  
Support multiple environments  
Version your API  
Set proper permissions  
Separate business logic  
Handle invalid input  
Avoid circular imports  
Test coverage regularly  
Use static analysis tools  
