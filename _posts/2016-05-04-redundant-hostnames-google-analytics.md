---
layout: post
title: "Dealing with duplicate content or redundant hostnames on GA"
date: 2016-05-04 00:00:00 +0100
tags: google analytics hostnames redundant
author: nicolaseckhart
---

### The issues
Google Analytics gives you a redundant hostnames warning, when your Website can be viewed under different URLs. In my case
the issue was, that you could view my application with or without prepending www to the domain name and the non-www version
didn't redirect the user. This is an issue for search engines, because the have two 'versions' and don't know which one to
list.

![](http://i.imgur.com/hhNUF7t.png)

Duplicate content is basically the same deal. It simply refers to a single page. For example if example.com/post-about-plugin
and example.com/posts/plugin have same content. The search engines won't know which one to list.

Both issues are bad for SEO, so it's best to try and get rid of them. Here's how:

### Solutions
There are several ways how to fix this, and they don't always all work:

#### 301 Redirect
An easy way for a webmaster to get rid of this warning, is to setup a 301 redirect for the user.
You can do this by editing the .htaccess file on your server. Here's a guide on doing it on an
apache server: http://www.rapidtables.com/web/dev/htaccess-redirect.htm
(Depending on how your DNS is setup, you can accomplish it with a CNAME record as well.)

#### Canonical Host
While the above way is best, there can be technical reasons why you cannot do a 301 redirect.
Thats where canonical host comes in. The rel=canonical element, often called the "canonical link",
is an HTML element that helps webmasters prevent duplicate content issues.
It does this by specifying the "canonical", or "preferred", version of a web page.

You start by picking one of your two pages as the canonical version. It should be the version you think is
the most important one. If you don't care, pick the one with the most links or visitors.
Then you add the following html tag into the `<head>` of the non-canonical version:

```html
<link rel="canonical" href="https://www.example.com/preffered_version">
```

This tells search engines which version of the two duplicates is the one that should be listed, without actually
redirecting the user. It's basically a "soft redirect".

The canonical host version works for single pages that have a duplicate, as well as for the www / non-www problem
I outlined above. Just just have to point to the preferred version from it's duplicate and the warning on Google Analytics
will be resolved.

#### Which one is better?
The answer is simple: **if there are no technical reasons not to do a redirect, you should always do a redirect.**
If you cannot redirect because that would break the user experience or be otherwise problematic: set a canonical URL.
