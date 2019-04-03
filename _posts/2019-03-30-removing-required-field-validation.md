---
layout: post
title: "Chrome DevTools: Required field validation"
description: 
headline: 
modified: 2019-03-30
category: Testing
tags: [Testing, DevTools, JavaScript]
imagefeature: 
mathjax: 
chart: 
comments: true
featured: true
---

Often when attempting to submit a form, if you choose to do so without inputting anything, you may find you are prompted to input a field value even before the form has been submitted. 

These inputs could be taking advantage of the *required* field attribute in an attempt to get users to input a value before they can submit the form.

![An example of removing required field attributes]({{ site.baseurl }}/images/Chrome DevTools Required field validation.gif)

### Removing required field attributes can help identify validation issues
Using the DevTools console you can execute some JavaScript which will remove all *required* attributes where they exist from elements within a form, allowing you to test validation.

### To execute the JavaScript snippet

1. Open DevTools within Chrome :
	* Windows: `CTRL+SHIFT+J` OR `F12`
	* Mac: `Command+Option+J`
	* You can also open through the wrench menu (Tools > JavaScript Console)

2. Paste the following snippet into the console tab and press `Enter` on your keyboard to execute the snippet on the web page you are currently viewing

`Array.prototype.slice.call (document.querySelectorAll('input, select')).map(function(el){el.removeAttribute('required')});`

The above snippet find's all elements within the currently loaded document (web page) and find's all elements of type *input* and *select*. For each element *(el)* which is found of these types, the *required* attribute is removed from the element.

Now when you submit the form either you will now get some other validation errors displayed or maybe the form will submit..

### Find this useful?

Why not check out the [UsefulJsSnippetExtension](https://github.com/eviltester/usefuljssnippetextension).