# Django REST

[TOC]



## serializer 

```python
from django.contrib.auth.models import User, Group
from rest_framework import serializers


class UserSerializer(serializers.HyperlinkedModelSerializer):
    class Meta:
        model = User
        fields = ('url', 'username', 'email', 'groups')


class GroupSerializer(serializers.HyperlinkedModelSerializer):
    class Meta:
        model = Group
        fields = ('url', 'name')
```

reswe create a new module named serializers.py in the app 

using hyperlinked relation in this case with HyperlinkedModelSerializer. You can also use primary key and other relationships 



## View 

originally, we can use the function for each method and use if-elif for each 'GEt', 'POST' etc. Using @api_view this decorator could allowed request.data to be parser. and we dont need to use JSONParser anymore 

also you need to use serializer to serialize the response, and also use serializer to check if the incoming 'PT' and 'POST' data if it is valid.

we can also use an class based view for each method and use function for each 'GET' and 'POST'. in urls file you need to check them into views.xxxx.as_view()







![44a3fbf4-0904-448b-88e1-d31c064b60aa.png](https://gallery.mailchimp.com/c4762c4571cf2c01957b7ce67/images/44a3fbf4-0904-448b-88e1-d31c064b60aa.png)