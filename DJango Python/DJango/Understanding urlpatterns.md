Suppose we have a file urls.py in our project. Lets look at the code in urls.py file of our project folder.

```
from django.conf.urls import include, url
from django.contrib import admin

urlpatterns = [
    
	url(r'^home/', include('myapp.urls')),
	
]
```

Now lets look at the line: 

`url(r'^home/', include('myapp.urls')),`

The first part is `r’^home/’`

Here,

`r` = the character **'r'** means regular expression. To write a regular expression in Django, we need to start with the character ‘r’ to tell Django that the following string is a regular expression.

`^` =  **'^'** means the beginning.

`^home/` = in Django URL resolvers, **"ht&#8203;tp://&#8203;127.0.0.1:8000/"** is not a part of the URL. So, **"^home/"** means that any Url that begins with **"home/"** . So **"ht&#8203;tp://&#8203;127.0.0.1:8000/home/"** is considered as only **"home/"** in Django and so the url:  **"ht&#8203;tp://&#8203;127.0.0.1:8000/home/"** will match the regular expression. 

The next part is `include(‘myapp.urls’)`

Here,

Django will now redirect everything that comes into **"ht&#8203;tp://&#8203;127.0.0.1:8000/home/"** to **myapp.urls** and look for further instructions there. 


Now lets look at the code in **myapp.urls** file:

```
from django.conf.urls import include, url
from . import views
urlpatterns = [
    url(r'^$', views.hello, name='hello'),
]
```
As you can see, we're now assigning a view called hello to the `^$` URL. This regular expression will match `^` (a beginning) followed by `$` (an end) – so only an empty string will match. That's correct, because in Django URL resolvers, **"ht&#8203;tp://&#8203;127.0.0.1:8000/"** is not a part of the URL. This pattern will tell Django that `views.hello` is the right place to go if someone enters your website at the **"ht&#8203;tp://&#8203;127.0.0.1:8000/"** address (By this I don’t mean that typing a url **"ht&#8203;tp://&#8203;127.0.0.1:8080/"** will take you to the desired page.). As we are entering the home page at the **"ht&#8203;tp://&#8203;127.0.0.1:8000/"** address, Django will take us to `views.hello` which is the place we want to go to retrieve our page’s contents.
 
So, the line : `url(r'^$', views.hello, name='hello')` has three parts:

First part tells the address. 

Second part tells where to look for contents.

The last part, name='hello', is the name of the URL that will be used to identify the view. So, our url - **(r'^$', views.hello)** now has a name called **hello**. So, in other parts of our project if we want to point to `r'^$'` or `views.hello` (By now, we know that both point to the same location because `r'^$'` will take us to `views.hello` which is the place we want to go to retrieve our page’s contents), we can do that by just typing the name of the url.  The name of the url can be the same as the name of the view but it can also be something completely different.It is important to name each URL in the app. We should also try to keep the names of URLs unique and easy to remember.

(Some contents are taken from online sources and modified)
