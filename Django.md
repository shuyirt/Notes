# Django

[TOC]

## Installation

### Install FCC

Either download Xcode and then get the Command Line Tools by running. 

```bash
$ python manage.py migrate		
```

or get a OSX-GCC-Installer package

### Install Homebrew

Open terminal and run 

```bash
$ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

```

Once you finished, insert the Homebrew directory at the top of your `PATH` environment variable. (not sure how this works)

```bash
$ export PATH="/usr/local/opt/python/libexec/bin:$PATH"
```

Comfirm Homebrew's installation

```bash
$ brew doctor
```

### Install Python 

Now, we can install Python 3:

```bash
$ brew install python
```

Confirm Python 

```bash
$ python3
```

get dependency manager

```bash
$ pip install --user pipenv
```

Get a new virtualenv

```bash
$ python3 -m virtualenv (name)
```

activate your virtual environment

```bash
$ source (name)/bin/activate
```

deactivate your veritual env

```bash
$ deactivate
```

### Install Django

in your virtual environment 

```bash
$ pip install Django
```

verify

```bash
$ python -m django --version
```

### Need a database

[database installation information](https://docs.djangoproject.com/en/2.1/topics/install/#database-installation)

run the Django command-line utility to create the database tables automatically

```bash
$ python manage.py migrate
```

## New Project

### creating a new project 

This will create a `mysite` directory in your current directory

```bash
$ django-admin startproject mysite
```

### creating a new app 

You need to be in the project directory 

```bash
$ python manage.py startapp polls
```

### run server 

```bash
$ python manage.py runserver serverIP:port
```

## Writing App

### Root URLconf

the root URLconf at the project's url file `mystic/urls.py` needs to be referenced to other URLconfs using  [`include()`](https://docs.djangoproject.com/en/2.1/ref/urls/#django.urls.include) 

```python
#mysite/mysite/urls.py¶
from django.contrib import admin
from django.urls import include, path

urlpatterns = [
    path('polls/', include('polls.urls')),
    path('admin/', admin.site.urls),
]
```

[`path()`](https://docs.djangoproject.com/en/2.1/ref/urls/#django.urls.path) is passed four arguments: route, view, kwargs, name 

- Route: a tring that contains a URL pattern 
- View: calls the specified view function with an [`HttpRequest`](https://docs.djangoproject.com/en/2.1/ref/request-response/#django.http.HttpRequest) object as the first argument and any “captured” values from the route as keyword arguments.
- Kwargs: Arbitrary keyword arguments can be passed in a dictionary to the target view
- Name: Naming your URL lets you refer to it unambiguously from elsewhere in Django, especially from within templates. This powerful feature allows you to make global changes to the URL patterns of your project while only touching a single file. 

### URLconf in App directory

create a URLconf in the polls firectory

```python 
#mysite/polls/urls.py¶
from django.urls import path

from . import views

urlpatterns = [
    path('', views.index, name='index'),
]
```

### create a view

```python 
# mysite/polls/views.py¶
from django.http import HttpResponse

def index(request):
    return HttpResponse("Hello, world. You're at the polls index.")
```



### creating models 

models are python classes need to be defined in `polls/models.py`

```python
#polls/models.py¶
from django.db import models

class Question(models.Model):
    question_text = models.CharField(max_length=200)
    pub_date = models.DateTimeField('date published')


class Choice(models.Model):
    question = models.ForeignKey(Question, on_delete=models.CASCADE)
    choice_text = models.CharField(max_length=200)
    votes = models.IntegerField(default=0)
```

### 

### Shell 

you can goes into the shell to try out Django API

```shell
$ python manage.py shell
```

Shell command

```
#import models
from polls.models import Choice, Question

#Query all Model object
Question.objects.all()

#new object
from django.utils import timezone
q = Question(question_text="What's new?", pub_date=timezone.now())
q.save

#access model field value 
q.question_text
q.pub_date

#edit model field value
q.question_text = "hey"
q.save()

#query
Question.objects.filter(question_text__startswith='What')
Choice.objects.filter(question__pub_date__year=timezone.now().year)

#get
from django.utils import timezone
current_year = timezone.now().year
Question.objects.get(pub_date__year=current_year)

#foreign key and set
c = q.choice_set.create(choice_text='Just hacking again', votes=0)
c.question
q.choice_set.all()

#delete
c = q.choice_set.filter(choice_text__startswith='Just hacking')
c.delete()
```

## Models

provides schema and each model maps to a single database table

The basics:

- Each model is a Python class that subclasses [`django.db.models.Model`](https://docs.djangoproject.com/en/2.1/ref/models/instances/#django.db.models.Model).
- Each attribute of the model represents a database field.
- With all of this, Django gives you an automatically-generated database-access API; see [Making queries](https://docs.djangoproject.com/en/2.1/topics/db/queries/).

### Quick Example

```python
from django.db import models

class Person(models.Model):
    first_name = models.CharField(max_length=30)
    last_name = models.CharField(max_length=30)
```

- it will have id as primary key 
- first name and last name as columns in table

you need to add your app into the `INSTALLED_APPS` in the `settings.py`

### Field

#### Field Type 

#### Field Option

| Field Options      | Description                                                  | Option            | Default                                                      |
| ------------------ | ------------------------------------------------------------ | ----------------- | ------------------------------------------------------------ |
| null               | Django will store empty values as `NULL` in the database.    | Boolean           | False                                                        |
| blank              | the field is allowed to be blank during validation           | Boolean           | False                                                        |
| choices            | If this is given, the default form widget will be a select box instead of the standard text field and will limit choices to the choices given.<br />the display value for a field with `choices` can be accessed using the [`get_FOO_display()`](https://docs.djangoproject.com/en/2.1/ref/models/instances/#django.db.models.Model.get_FOO_display)method. | a list or a tuple |                                                              |
| default            | the default value for the field. This can be a value or a callable object. If callable it will be called every time a new object is created. | Str               |                                                              |
| Help_text          | Extra “help” text to be displayed with the form widget. It’s useful for documentation even if your field isn’t used on a form. | Str               |                                                              |
| Primary_key        | if `True`, this field is the primary key for the model.<br />if not specify `primary_key=True`, Django will automatically add an [`IntegerField`](https://docs.djangoproject.com/en/2.1/ref/models/fields/#django.db.models.IntegerField)to hold the primary key | Boolean           | [Automatic primary key fields](https://docs.djangoproject.com/en/2.1/topics/db/models/#automatic-primary-key-fields) |
| unique             | If `True`, this field must be unique throughout the ta       | Boolean           |                                                              |
| verbose field name | Each field type, except for [`ForeignKey`](https://docs.djangoproject.com/en/2.1/ref/models/fields/#django.db.models.ForeignKey), [`ManyToManyField`](https://docs.djangoproject.com/en/2.1/ref/models/fields/#django.db.models.ManyToManyField) and [`OneToOneField`](https://docs.djangoproject.com/en/2.1/ref/models/fields/#django.db.models.OneToOneField), takes an optional first positional argument – a verbose name.<br />[`ForeignKey`](https://docs.djangoproject.com/en/2.1/ref/models/fields/#django.db.models.ForeignKey), [`ManyToManyField`](https://docs.djangoproject.com/en/2.1/ref/models/fields/#django.db.models.ManyToManyField) and [`OneToOneField`](https://docs.djangoproject.com/en/2.1/ref/models/fields/#django.db.models.OneToOneField) require the first argument to be a model class, so use the [`verbose_name`](https://docs.djangoproject.com/en/2.1/ref/models/fields/#django.db.models.Field.verbose_name) keyword argument: | Str               | automatically create it using the field’s attribute name, converting underscores to spaces. |

```
# example for choices
from django.db import models

class Person(models.Model):
    SHIRT_SIZES = (
        ('S', 'Small'),
        ('M', 'Medium'),
        ('L', 'Large'),
    )
    name = models.CharField(max_length=60)
    shirt_size = models.CharField(max_length=1, choices=SHIRT_SIZES)
```

### Relationship 

#### Many to one relationship

To define a many-to-one relationship, use [`django.db.models.ForeignKey`](https://docs.djangoproject.com/en/2.1/ref/models/fields/#django.db.models.ForeignKey).

```python
from django.db import models

class Manufacturer(models.Model):
    # ...
    pass

class Car(models.Model):
    manufacturer = models.ForeignKey(Manufacturer, on_delete=models.CASCADE)
    # ...
```

the name of a [`ForeignKey`](https://docs.djangoproject.com/en/2.1/ref/models/fields/#django.db.models.ForeignKey) field (`manufacturer` in the example above) be the name of the model, lowercase.

#### many to many relationship 

To define a many-to-many relationship, use [`ManyToManyField`](https://docs.djangoproject.com/en/2.1/ref/models/fields/#django.db.models.ManyToManyField). 

```python
from django.db import models

class Topping(models.Model):
    # ...
    pass

class Pizza(models.Model):
    # ...
    toppings = models.ManyToManyField(Topping)
```

It’s suggested, but not required, that the name of a [`ManyToManyField`](https://docs.djangoproject.com/en/2.1/ref/models/fields/#django.db.models.ManyToManyField) (`toppings` in the example above) be a plural describing the set of related model objects.

 There is a many-to-many relationship between a person and the groups of which they are a member, so you could use a[`ManyToManyField`](https://docs.djangoproject.com/en/2.1/ref/models/fields/#django.db.models.ManyToManyField) to represent this relationship. However, there is a lot of detail about the membership that you might want to collect, such as the date at which the person joined the group.

For these situations, Django allows you to specify the model that will be used to govern the many-to-many relationship. You can then put extra fields on the intermediate model. The intermediate model is associated with the[`ManyToManyField`](https://docs.djangoproject.com/en/2.1/ref/models/fields/#django.db.models.ManyToManyField) using the [`through`](https://docs.djangoproject.com/en/2.1/ref/models/fields/#django.db.models.ManyToManyField.through) argument to point to the model that will act as an intermediary. For our musician example, the code would look something like this:

```python
from django.db import models

class Person(models.Model):
    name = models.CharField(max_length=128)

    def __str__(self):
        return self.name

class Group(models.Model):
    name = models.CharField(max_length=128)
    members = models.ManyToManyField(Person, through='Membership')

    def __str__(self):
        return self.name

class Membership(models.Model):
    person = models.ForeignKey(Person, on_delete=models.CASCADE)
    group = models.ForeignKey(Group, on_delete=models.CASCADE)
    date_joined = models.DateField()
    invite_reason = models.CharField(max_length=64)
```



## Database

### Wire Database 

By default, the Djando configuration uses SQLite, and you don't need to install it 

If you want to use another database, you need to install appropriate [database bindings](https://docs.djangoproject.com/en/2.1/topics/install/#database-installation) and change keys DATABASES in `mysite/settings`. 

Check [`DATABASES`](https://docs.djangoproject.com/en/2.1/ref/settings/#std:setting-DATABASES) for reference

create the tagles in teh database before we can use them 

```bash
$ python manage.py migrate	
```

migrate command looks at the installed_apps settingn and create any necessary databese table accoding to the databse settins in you `mystic/settings.py` file and the data baseball migration shipped with the app

it supports common database relationships: many to one, many to many, and one to one

### Migration

1. make change
2. add polls app `polls.apps.PollsConfig` into installed_apps 

```bash
$ python mange.py makemigrations polls
```

`makemigrations` tells Djanfo that you made some change to your madels 

3. optional*:  prints it to the screen so that you can see what SQL Django thinks is required.

```bash
$ python manage.py sqlmigrate polls 0001
```

4. apply change to database

```bash
$ python manage.py migrate
```

### Don't repeat yourself (DRY)

## Admin & User

we need to create a user who can login to the admin site

```bash
$ python manage.py createsuperuser
```

then run server and login into the admin system by going into [http://127.0.0.1:8000/admin/](http://127.0.0.1:8000/admin/)

you can see groups and users which is provided by `Django.contrib.auth`

### make the app modifiable in the admin 

tell the admin that the model object have an admin interface 

open the `polls/admin.py`

```python
from django.contrib import admin

from .models import Question

admin.site.register(Question)
```

regiester the model into the admin page 

admin page has many short cut for modify the keys

## Template

create a template directory in your app director `polls/templates/polls/index.html`

Your project’s [`TEMPLATES`](https://docs.djangoproject.com/en/2.1/ref/settings/#std:setting-TEMPLATES) setting describes how Django will load and render templates. The default settings file configures a `DjangoTemplates` backend whose [`APP_DIRS`](https://docs.djangoproject.com/en/2.1/ref/settings/#std:setting-TEMPLATES-APP_DIRS) option is set to `True`. By convention `DjangoTemplates`looks for a “templates” subdirectory in each of the [`INSTALLED_APPS`](https://docs.djangoproject.com/en/2.1/ref/settings/#std:setting-INSTALLED_APPS).

then we can get the template and render it

```python
#polls/views.py
from django.http import HttpResponse
from django.template import loader

from .models import Question

def index(request):
    latest_question_list = Question.objects.order_by('-pub_date')[:5]
    template = loader.get_template('polls/index.html')
    context = {
        'latest_question_list': latest_question_list,
    }
    return HttpResponse(template.render(context, request))
```

or do this, a short cut for render()

```python
#polls/views.py¶
from django.shortcuts import render

from .models import Question

def index(request):
    latest_question_list = Question.objects.order_by('-pub_date')[:5]
    context = {'latest_question_list': latest_question_list}
    return render(request, 'polls/index.html', context)
```

Note that once we’ve done this in all these views, we no longer need to import [`loader`](https://docs.djangoproject.com/en/2.1/topics/templates/#module-django.template.loader) and [`HttpResponse`](https://docs.djangoproject.com/en/2.1/ref/request-response/#django.http.HttpResponse) (you’ll want to keep `HttpResponse` if you still have the stub methods for `detail`, `results`, and `vote`).

The [`render()`](https://docs.djangoproject.com/en/2.1/topics/http/shortcuts/#django.shortcuts.render) function takes the request object as its first argument, a template name as its second argument and a dictionary as its optional third argument. It returns an [`HttpResponse`](https://docs.djangoproject.com/en/2.1/ref/request-response/#django.http.HttpResponse) object of the given template rendered with the given context.

## raise error 

we can import `from django.http import Http404` and raise an error `raise Http404("Question does not exist")`

or use a short cut

`from django.shortcuts import get_object_or_404`

and 

`question = get_object_or_404(Question, pk=question_id)`

## Views

1. need csrf-token verification for form submit 
2. `request.POST['choice']` will raise [`KeyError`](https://docs.python.org/3/library/exceptions.html#KeyError) if `choice` wasn’t provided in POST data. 
3. you should always return an [`HttpResponseRedirect`](https://docs.djangoproject.com/en/2.1/ref/request-response/#django.http.HttpResponseRedirect) after successfully dealing with POST data. This tip isn’t specific to Django; it’s just good Web development practice.
4. We are using the [`reverse()`](https://docs.djangoproject.com/en/2.1/ref/urlresolvers/#django.urls.reverse) function in the [`HttpResponseRedirect`](https://docs.djangoproject.com/en/2.1/ref/request-response/#django.http.HttpResponseRedirect) constructor in this example. This function helps avoid having to hardcode a URL in the view function. It is given the name of the view that we want to pass control to and the variable portion of the URL pattern that points to that view.

5. generic views: less code is better
   1. why we use it : a common case of basic Web development: getting data from the database according to a parameter passed in the URL, loading a template and returning the rendered template. Because this is so common, Django provides a shortcut, called the “generic views” system.
   2. Convert 
      1. convert the URLconf
      2. Delete some of the old unneeded views
      3. introduce new views inherited from the Djando's generic view

## Test

create a test case in the tests.py file and 

run 

```bash
$ python manage.py test polls
```

will look for tests in the polls application 

## Static File System 

static files consist pictures and stylesheets

create a `static` directory in the `polls` directory 