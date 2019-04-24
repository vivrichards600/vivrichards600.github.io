---
layout: post
title: "Chrome DevTools: Identifying elements which are not displayed as expected"
description: 
headline: 
modified: 2019-04-03
category: Testing
tags: [Testing, DevTools, JavaScript]
imagefeature: 
mathjax: 
chart: 
comments: true
featured: true
---

Sometimes elements may be styled with a fixed width. The problem with this is if you change the text to be displayed within the styled element, for example changing the language you wish to view the website in, then some of the text may not be displayed as expected.

![Example of identifying a link styled with a fixed width with text which isn't displayed as expected]({{ site.baseurl }}/images/Chrome DevTools Test Text Length.gif)

### Identifying links styled with a fixed width where text may not be displayed as expected 
Using the DevTools console you can execute some JavaScript which will increase a links text length in order to identify links where their text length exceeds the fixed width which is set for it.

### To execute the JavaScript snippet

1. Open DevTools within Chrome :
	* Windows: `CTRL+SHIFT+J` OR `F12`
	* Mac: `Command+Option+J`
	* You can also open through the wrench menu (Tools > JavaScript Console)

2. Paste the following snippet into the console tab and press `Enter` on your keyboard to execute the snippet on the web page you are currently viewing

<script src="https://gist.github.com/vivrichards600/c26d5e81c08baa94df0cdf0566ceb27c.js"></script>

The above snippet find's all *a* (links) within the currently loaded document (web page). For each *link* which is found, we then loop through each *link* on the loaded document and increase it's text length by appending a random string to the end of it.

### Find this useful?

Why not check out the [UsefulJsSnippetExtension](https://github.com/eviltester/usefuljssnippetextension).
