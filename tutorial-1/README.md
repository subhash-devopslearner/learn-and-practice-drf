# Tutorial Number - 1  

## This tutorial is prepared from following source:

[Django Rest Framework - Quickstart (https://www.django-rest-framework.org/tutorial/quickstart/#quickstart)](https://www.django-rest-framework.org/tutorial/quickstart/#quickstart)

## Initial Steps - 

`cd tutorial-1/`   
 `django-admin startproject tutorial .`   
 `cd tutorial/`  
 `django-admin startapp quickstart`  
 `python manage.py migrate`  
 `django-admin createsuperuser --username admin --email admin@example.com`  
 `python manage.py runserver`  


On command line check -   
`curl 'Accept: application/json; indent=4' http://127.0.0.1:8000/users/`  

Or in browser, open `http://127.0.0.1:8000/users/`