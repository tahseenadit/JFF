Suppose our file tree is:

```
examplapp/
  __init__.py
  templatetags/
    __init__.py
    index.py
  models.py
  views.py

```
As stated in the django documentation:

The most common place to specify custom template tags and filters is inside a Django app. If they relate to an existing app, it makes sense to bundle them there; otherwise, they can be added to a new app. When a Django app is added to INSTALLED_APPS, any tags it defines in the conventional location described below are automatically made available to load within templates.

The app should contain a templatetags directory, at the same level as models.py, views.py, etc. If this doesn’t already exist, create it - don’t forget the __init__.py file to ensure the directory is treated as a Python package.

Here **exampleapp** is an app name of our project. **index.py**,**views.py**,**models.py**,**__init.py** are module names. Our app **exampleapp** contains a templatetags directory, at the same level as **models.py,views.py,etc**. We have also added **__init.py__** in our templatetags directory so that the directory is treated as a python package. 

our custom tags and filters will live inside the **index.py** module. We have named our module as **index** but we can give any name to our module, but we need to be careful that the name is unique and does not conflict with other custom tags and filters module in another app of our project. We will use the name of our module to load the tags in our html file. 

