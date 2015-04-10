---
layout: post
title:  "Introducing MaterialDjango & tinylibrary"
date:   2015-04-10 18:00:00
categories: django update tinylibrary shipit
---

There isn't yet a MaterialDjango [Google's Material Design for django], but there is tinylibrary a lab for me to prototype stuff for the big Pizza Cat release that's around the corner.*

[Tinylibrary](https://github.com/Colorless-Green-Ideas/tinylibrary) ([demo on heroku](https://tinylibrary.herokuapp.com/books/)) is a tool to track libraries that aren't big enough to merit running dedicated library systems or working out logins. Just add it on to a django site! (Or run ours. Runs with [Whitenoise](https://warehouse.python.org/project/whitenoise/) for heroku-approved static files with gzip) We're using [Google's Polymer library](https://www.polymer-project.org/0.5/) for an IE shim for webcomponents and then the paper-ui library built upon it. But we don't use Polymer's MVC bending templating. Django does the "hard work" we're just here to take Paper-UI niceness for "free."

MaterialDjango sports a subset of widgets, expanding slowly, currently:

- TextInputs with PaperTextInput
- PasswordInputs with PaperPasswordInput

{% highlight python %}
#forms.py
from django import forms
from materialdjango.widgets import PaperTextInput
class BookForm(forms.ModelForm):
    class Meta:
        model = Book
        labels={'title': '',
                'isbn': '',
                'author': '',}
        widgets = {
            'title': PaperTextInput,
            'isbn' : PaperTextInput,
            'author': PaperTextInput,
        }
{% endhighlight %}
or
{% highlight python %}
#forms.py
from django.forms.models import modelform_factory
from materialdjango.forms import mangle_form

BookForm = mangle_form(modelform_factory(Book,fields="__all__"))

{% endhighlight %}

- [Vulcanization](http://docs.polymerchina.org/articles/concatenating-web-components.html) if you don't have a npm/bower stack dev dependency
- A pleasantly simple (30~ LOC vulcanized) base.html to use for rapid prototyping
- Cleaned up imports, managed assets
{% highlight html %} 
{%raw%}
{% load staticfiles %}
{% load polymerdep %}
<html>
<head>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="Content-Type" content="text/html;charset=utf-8" />
    <script src={{"{% static 'materialdjango/components/bower_components/webcomponentsjs/webcomponents.js' }}%}"></script>
    {{ "polymer/polymer.html" | dep}}
    {{ "core-scaffold/core-scaffold.html" | dep}}
<...>
{%endraw%}
{% endhighlight %}
- Easy compatability with next Polymer release because we don't use any of the internals!
- Don't write CSS unless you have to.


