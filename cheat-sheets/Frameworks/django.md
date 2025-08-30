# DJANGO

Django — потужний Python-фреймворк для швидкої розробки веб-додатків з ORM, шаблонами, роутингом, middleware, адмінкою, авторизацією та багатьма вбудованими інструментами.

## Категорія: Встановлення та старт

| Команда/метод                    | Опис                 | Приклад/Аутпут                   |
| -------------------------------- | -------------------- | -------------------------------- |
| pip install django               | встановити Django    | pip install django               |
| django-admin startproject        | створити проект      | django-admin startproject mysite |
| python manage.py startapp        | створити додаток     | python manage.py startapp blog   |
| python manage.py runserver       | запуск dev-сервера   | python manage.py runserver       |
| python manage.py migrate         | застосувати міграції | python manage.py migrate         |
| python manage.py makemigrations  | створити міграції    | python manage.py makemigrations  |
| python manage.py createsuperuser | створити адміна      | python manage.py createsuperuser |
| python manage.py shell           | інтерактивна консоль | python manage.py shell           |

## Категорія: Структура проекту

| Файл/папка      | Опис               | Приклад/Аутпут                  |
| --------------- | ------------------ | ------------------------------- |
| manage.py       | керування проектом | python manage.py ...            |
| settings.py     | налаштування       | DEBUG = True                    |
| urls.py         | роутинг            | path('admin/', admin.site.urls) |
| wsgi.py/asgi.py | сервер             | wsgi.py, asgi.py                |
| app/models.py   | моделі             | class Post(models.Model): ...   |
| app/views.py    | представлення      | def index(request): ...         |
| app/templates/  | шаблони            | templates/index.html            |
| app/static/     | статика            | static/style.css                |

## Категорія: Моделі та ORM

| Команда/метод                           | Опис                  | Приклад/Аутпут                                             |
| --------------------------------------- | --------------------- | ---------------------------------------------------------- |
| class X(models.Model)                   | модель                | class Post(models.Model): ...                              |
| models.CharField(max_length)            | рядок                 | title = models.CharField(max_length=100)                   |
| models.IntegerField()                   | число                 | views = models.IntegerField()                              |
| models.DateTimeField(auto_now_add=True) | дата/час              | created = models.DateTimeField(auto_now_add=True)          |
| models.ForeignKey                       | зовнішній ключ        | author = models.ForeignKey(User, on_delete=models.CASCADE) |
| models.ManyToManyField                  | багато-до-багатьох    | tags = models.ManyToManyField(Tag)                         |
| objects.create/get/filter               | CRUD                  | Post.objects.create(...), .get(), .filter()                |
| .save(), .delete()                      | зберегти/видалити     | post.save(), post.delete()                                 |
| .all(), .first(), .last()               | вибірка               | Post.objects.all().first()                                 |
| .order_by(), .count()                   | сортування/підрахунок | .order_by('-date'), .count()                               |
| Q(), F()                                | складні запити        | Q(title\_\_icontains='a')                                  |

## Категорія: Міграції та адміністрування

| Команда/метод               | Опис                 | Приклад/Аутпут                   |
| --------------------------- | -------------------- | -------------------------------- |
| makemigrations, migrate     | міграції             | python manage.py makemigrations  |
| createsuperuser             | створити адміна      | python manage.py createsuperuser |
| admin.site.register         | реєстрація моделі    | admin.site.register(Post)        |
| @admin.register             | декоратор            | @admin.register(Post)            |
| list_display, search_fields | налаштування адмінки | list_display = ('title',)        |

## Категорія: В’юхи, роутинг, шаблони

| Команда/метод              | Опис                  | Приклад/Аутпут                         |
| -------------------------- | --------------------- | -------------------------------------- |
| def view(request): ...     | функція-представлення | def index(request): ...                |
| render(request, tpl, ctx)  | рендер шаблону        | render(request, 'index.html', {...})   |
| path(), re_path()          | роутинг               | path('blog/', views.index)             |
| include()                  | вкладені урли         | path('blog/', include('blog.urls'))    |
| {% ... %}, {{ ... }}       | шаблони Django        | {% for p in posts %} ... {{ p.title }} |
| {% url 'name' %}           | згенерувати url       | <a href="{% url 'home' %}">            |
| {% extends %}, {% block %} | наслідування шаблонів | {% extends 'base.html' %}              |

## Категорія: Форми, валідація, авторизація

| Команда/метод                | Опис                 | Приклад/Аутпут                       |
| ---------------------------- | -------------------- | ------------------------------------ |
| forms.Form, forms.ModelForm  | форми                | class PostForm(forms.ModelForm): ... |
| form.is_valid(), form.save() | валідація/збереження | if form.is_valid(): form.save()      |
| request.user, login, logout  | користувач/логін     | login(request, user)                 |
| @login_required              | захист в’юхи         | @login_required                      |
| messages.success             | флеш-повідомлення    | messages.success(request, 'OK')      |

## Категорія: Middleware, signals, API

| Команда/метод     | Опис             | Приклад/Аутпут                                         |
| ----------------- | ---------------- | ------------------------------------------------------ |
| middleware        | проміжний шар    | class MyMW: ... **call**(self, req)                    |
| signals.post_save | сигнал           | from django.db.models.signals import post_save         |
| @receiver         | обробник сигналу | @receiver(post_save, sender=Post)                      |
| rest_framework    | API              | from rest_framework import viewsets                    |
| serializers       | серіалізація     | class PostSerializer(serializers.ModelSerializer): ... |
| @api_view         | API-функція      | @api_view(['GET'])                                     |

## Категорія: Тести, best practices

| Команда/метод           | Опис               | Приклад/Аутпут                   |
| ----------------------- | ------------------ | -------------------------------- |
| TestCase, Client        | тести              | from django.test import TestCase |
| client.get('/url/')     | HTTP-запит у тесті | client.get('/blog/')             |
| assertEqual, assertTrue | перевірки          | self.assertEqual(x, 1)           |
| coverage, flake8, black | якість коду        | coverage run, flake8, black      |
| .env, settings.py       | змінні оточення    | SECRET_KEY = ...                 |
| Документація            | help(), docstring  | help(Post), def f(): """doc"""   |

---

> Шпаргалка складена за інструкціями: компактно, категоріями, з короткими прикладами та описами.
