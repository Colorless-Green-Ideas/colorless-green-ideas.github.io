---
layout: post
title:  "Introducing MaterialDjango via tinylibrary"
date:   2015-03-20 24:00:00
categories: django update tinylibrary
---

There isn't yet a MaterialDjango [Google's Material Design for django], but there is tinylibrary a lab for me to prototype stuff for the big Pizza Cat release that's around the corner.*

Tinylibrary is a tool to track libraries that aren't big enough to merit running dedicated library systems or working out logins. Just add it on to a django site! (Or run ours. Runs with Whitenoise for heroku-approved static files with gzip) We're using Google's Polymer library for an IE shim for webcomponents and then the paper-ui library built upon it. But we don't use Polymer's MVC bending templating. Django does the "hard work" we're just here to take Paper-UI niceness for "free."

MaterialDjango would support currently:

- TextInputs with PaperTextInput 
{% highlight python %}
#forms.py
from django import forms
from widgets import PaperTextInput
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
- [Vulcanization](http://docs.polymerchina.org/articles/concatenating-web-components.html) if you don't have a npm/bower stack dev dependency
- A pleasantly simple (30~ LOC vulcanized) base.html to use for rapid prototyping
- Easy compatability with next Polymer release because we don't use any of the internals!
- Don't write CSS unless you have to.


Check out the [Jekyll docs][jekyll] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll's GitHub repo][jekyll-gh].

*Valve time may apply.

[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll]:    http://jekyllrb.com
