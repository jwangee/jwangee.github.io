---
title: "Write A New Blog or Projects Post"
layout: post
date: 2017-07-22 20:10
tag: 
- Jekyll tutorial
star: true
image: /assets/images/profile_2.jpg
headerImage: true
projects: false
blog: true
category: blog
author: Jianfeng
description: Jekyll - how to write a new post
externalLink: false
---

## Summary

This post is created to show how to write a new blog/project post by using Markdown.<br/>
I should pick items up from the following lists.
### Common Elements from Markdown
- [Heading](#heading)
- [Quote](#quote)
- [Unordered/Ordered Lists](#lists)
- [URL](#url)
- [Images](#images)
- [Code](#code)

---

## Heading
There are six levels of headings. They correspond with the six levels of HTML headings. Each level down uses one more hash character. I decide to use 4 of them at most.
{% highlight raw %}
# Heading
## Heading
### Heading
#### Heading
{% endhighlight %}

### The sub-chapter
I may have to use a lot of sub-chapters.
{% highlight raw %}
<code here>
## Heading
{% endhighlight %}

### Paragraph
{% highlight raw %}
<p></p> to create a paragraph.
<br> or <br/> to output a end-of-line.
{% endhighlight %}

---

## Quote
Here are what the quote looks like and how I create a quote.
> Here is a quote...
{% highlight raw %}
<code here>
> Here is a quote...
{% endhighlight %}

---

## Lists
### A Unordered list
* An item
* Another item
* Yet another item
* And there's more...

{% highlight raw %}
* An item
* Another item
* Yet another item
* And there's more...
{% endhighlight %}
### An ordered list
1. Item 1
2. A second item
3. Number 3

{% highlight raw %}
1. Item 1
2. A second item
3. Number 3
{% endhighlight %}

---

## URL

URLs can be added in a easy way.<br/>
Here is a link to an external website. [Jianfeng](http://google.com/)
{% highlight raw %}
<code here>
[Jianfeng](http://google.com/)
{% endhighlight %}

---

## Images
Adding images should be similar to adding an external URL.
{% highlight raw %}
<code here>
![Markdowm Image][image/url]
{% endhighlight %}
![Markdowm Image][1]
<figcaption class="caption">Photo from the Internet</figcaption>
Also, I can add a title for the image.
{% highlight raw %}
<code here>
<figcaption class="caption">Photo from the Internet</figcaption>
{% endhighlight %}

---

## Code
We can use the following 'highlight' tag to show code.<br/>
{% highlight raw %}
{%raw%}{% highlight xx-language %}{%endraw%}
Write the code here
{%raw%}{% endhighlight %}{%endraw%}
{% endhighlight %}
Here is an example for HTML.
{% highlight html %}
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
</head>
<body>
    <h1>Just a test</h1>
</body>
</html>
{% endhighlight %}
Here is an example for Python.
{% highlight python %}
import sys
print "Hello world!"
{% endhighlight %}

[1]: http://kune.fr/wp-content/uploads/2013/10/ghost-blog.jpg
