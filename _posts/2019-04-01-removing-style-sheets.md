---
layout: post
title: "Chrome DevTools: No Styles"
description: 
headline: 
modified: 2019-04-01
category: Accessibility
tags: [Testing, DevTools, JavaScript, Accessibility]
imagefeature: 
mathjax: 
chart: 
comments: true
featured: true
---

When it comes to ensuring your web applications are accessibile to all, one of the checks you may wish to carry out is to see how your page is displayed with stylesheets disabled. 

Viewing a web page this way represents the underling reading and navigation order, the order in which keyboard-only and screen reader users will access the page.

![An example of disabling page styles]({{ site.baseurl }}/images/Chrome DevTools no styles.gif)

### Disabling stylesheets
Using the DevTools console you can execute some JavaScript which will disable all stylesheets, allowing you to test the reading and navigation order.

### To execute the JavaScript snippet

1. Open DevTools within Chrome :
	* Windows: `CTRL+SHIFT+J` OR `F12`
	* Mac: `Command+Option+J`
	* You can also open through the wrench menu (Tools > JavaScript Console)

2. Paste the following snippet into the console tab and press `Enter` on your keyboard to execute the snippet on the web page you are currently viewing

`Array.prototype.slice.call (document.styleSheets).map(function(el){el.disabled = true;});`

The above snippet find's all stylesheets within the currently loaded document (web page). For each stylesheet *(el)* which is found, the stylesheet is then disabled.

### Find this useful?

Why not check out the [UsefulJsSnippetExtension](https://github.com/eviltester/usefuljssnippetextension).