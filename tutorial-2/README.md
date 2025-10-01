# Tutorial Number - 1  

## This tutorial is prepared from following source:

[Django Rest Framework - Tutorial 1 (https://www.django-rest-framework.org/tutorial/1-serialization/)](https://www.django-rest-framework.org/tutorial/1-serialization/)

## Initial Steps - 

`cd tutorial-2/`   
`django-admin startproject tutorial .`      
`django-admin startapp snippets`  
`pip install -r ../requirements.txt`   
`python manage.py makemigrations`  
`python manage.py migrate`  
`python manage.py shell`  


***Serialize instance***
```
from snippets.models import Snippet
from snippets.serializers import SnippetSerializer
from rest_framework.renderers import JSONRenderer
from rest_framework.parsers import JSONParser

snippet = Snippet(code='foo = "bar"\n')
snippet.save()

snippet = Snippet(code='print("hello, world")\n')
snippet.save()

# Output
serializer = SnippetSerializer(snippet)
serializer.data
# {'id': 2, 'title': '', 'code': 'print("hello, world")\n', 'linenos': False, 'language': 'python', 'style': 'friendly'}

content = JSONRenderer().render(serializer.data)
content
# b'{"id":2,"title":"","code":"print(\\"hello, world\\")\\n","linenos":false,"language":"python","style":"friendly"}'
```

***Derialize instance***
```
import io

stream = io.BytesIO(content)
data = JSONParser().parse(stream)

serializer = SnippetSerializer(data=data)
serializer.is_valid()
# True
serializer.validated_data
# {'title': '', 'code': 'print("hello, world")', 'linenos': False, 'language': 'python', 'style': 'friendly'}
serializer.save()
# <Snippet: Snippet object>

serializer = SnippetSerializer(Snippet.objects.all(), many=True)
serializer.data
# [{'id': 1, 'title': '', 'code': 'foo = "bar"\n', 'linenos': False, 'language': 'python', 'style': 'friendly'}, {'id': 2, 'title': '', 'code': 'print("hello, world")\n', 'linenos': False, 'language': 'python', 'style': 'friendly'}, {'id': 3, 'title': '', 'code': 'print("hello, world")', 'linenos': False, 'language': 'python', 'style': 'friendly'}]
```



