---
layout: post
title: "Chrome DevTools: Identifying form inputs with no labels"
description: 
headline: 
modified: 2019-04-03
category: Accessibility
tags: [Testing, DevTools, JavaScript, Accessibility]
imagefeature: 
mathjax: 
chart: 
comments: true
featured: true
---

When developing web applications, they should be accessible to all. When you want to ensure your web application is accessible a check you will want to do is to ensure each form input element has established label relationship.

> "When labels *for* form elements are absent, screen reader users do not know the *input* data expectations. Screen readers cannot programmatically determine information about *input* objects without an established *label* relationship (or redundant text serving as a label)." - [Deque University](https://dequeuniversity.com/rules/axe/3.1/label?application=lighthouse)

![Example of identifying an input without an associated label]({{ site.baseurl }}/images/Chrome DevTools input no label.gif)

### Identifying inputs with no established label relationship
Using the DevTools console you can execute some JavaScript which will highlight any *input* which does not have a *label* associated with it.

### To execute the JavaScript snippet

1. Open DevTools within Chrome :
	* Windows: `CTRL+SHIFT+J` OR `F12`
	* Mac: `Command+Option+J`
	* You can also open through the wrench menu (Tools > JavaScript Console)

2. Paste the following snippet into the console tab and press `Enter` on your keyboard to execute the snippet on the web page you are currently viewing

<script class="notepad-post-content post" src="https://gist.github.com/vivrichards600/7032395fe59d345d3a0163213e054fa3.js"></script>

The above snippet find's all *inputs* and *labels* within the currently loaded document (web page). For each *input* which is found, we then loop through each *label* on the loaded document and check it's *for* attribute. If we do not find any labels that have a *for* attribute that matches any input *id* we then know we've found a form input without a corresponding label. The *for* attribute's value of a label must be the *id* of the input it is associated with.

### Find this useful?

Why not check out the [UsefulJsSnippetExtension](https://github.com/eviltester/usefuljssnippetextension).