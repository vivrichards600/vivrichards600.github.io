---
layout: post
title: Automating visual checking of alt tags, labels, broken links and duplicate ids
description: 
headline: 
modified: 2018-11-06
category: Automation
tags: [accessibility testing, visual testing, usability, automation]
imagefeature: 
mathjax: 
chart: 
comments: true
featured: true
---

This week I was [mentioned in a tweet by Wim Selles](https://twitter.com/wswebcreation/status/1230769653007310851).

Wim had written some code to do an image comparison of a pages tabbability which is something I had blogged and spoken about before at various events. [I have previously also written how visual checking could help check pdfs, tabbability for accessibility and chart rendering](http://localhost:4000/testing/visual-testing-digging-deeper) but the tweet got me thinking, what other things could visual checking assist with when checking web pages?

I'm a contributor to the [useful snippets Chrome extension created by the awesome Alan Richardson](https://github.com/eviltester/usefuljssnippetextension) and within this extension together we have written lots of really cool (if I do say so myself) snippets and so I wanted to see if any could be used along with visual checking to get quicker feedback when things don't look or perhaps work as we expected.

The things I wanted to check and highlight in my visual checks were:
* Are there any images on my page with no alt tags
* Are there any inputs on my page which do not have associated labels
* Are there any broken links on my page
* Are there any elements on my page with the same ids

If any of the above were true I decided that I would draw a pink border around the problems. In reality you may want to do something like add text or an icon to highlight what type of issue was found but I decided to keep this proof of concept fairly simple.

Using the [visual testing code](https://github.com/vivrichards600/AutomatedVisualTesting) example project I have made on GitHub I wrote a very quick and dirty test to check the above (no alt tags, inputs with no labels, broken links).

![_config.yml]({{ site.baseurl }}/images/a11y-issues.png)

Below is the rather ugly but working code I created which enabled me to do the above visual checks.
<script src="https://gist.github.com/vivrichards600/f324c3801529dbaf3e66cf327c25b2d2.js"></script>

Ideally you'd use this code within something like [AppliTools](https://applitools.com/) which is in my opinion the best visual checking tool but at the end of the day all we are doing here is injecting JavaScript in to a page via the browsers `ExecuteJavaScript` method so you could try this with any visual checking framework - but your results may or may not be as good.

I have not updated the [visual testing code](https://github.com/vivrichards600/AutomatedVisualTesting) project with this example but wanted to share this idea to get people to start thinking about other ways that visual testing could be really useful!

As always any feedback and comments are welcome.