# Routing class

One of the most advanced features of DJango is the use of class to manage a response.  Our class needs to inherited from `Django.views.View` class. And we need to have care about how to use it in the `url.py` file.

In the `url.py` file need to be added as:
```python
path('main', views.MainView.as_view()),
```

In the `views.py` file must to be declared as:

```python
from django.http import HttpResponse
from django.utils.html import escape
from django.views import View

class MainView(View) :
    def get(self, request):
        response = """<html><body><p>Hello world MainView in HTML</p>
        <p>This sample code is available at
        <a href="https://github.com/csev/dj4e-samples">
        https://github.com/csev/dj4e-samples</a></p>
        </body></html>"""
        return HttpResponse(response)

```

## passing parameterss to view class

The way to pass parameter to a class is the next

```
https://samples.dj4e.com/views/remain/abc123-42-xyzzy 

```

Here the syntax is very similar to a fucntion with parameters. Note that slung type is kind of string.

```python
path('remain/<slug:guess>', views.RestMainView.as_view()),

```

The parameter is passed as a third paramer of the in the get method of the class.

```python
from django.http import HttpResponse
from django.utils.html import escape
from django.views import View

class RestMainView(View) :
    def get(self, request, guess):
        response = """<html><body>
        <p>Your guess was """+escape(guess)+"""</p>
        </body></html>"""
        return HttpResponse(response)

```