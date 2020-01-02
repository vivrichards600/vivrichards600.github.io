---
layout: post
title: Automating page tabability (is that a word?) with visual testing
description: 
headline: 
modified: 2018-11-06
category: Accessibility
tags: [accessibility testing, visual testing, usability, automation]
imagefeature: 
mathjax: 
chart: 
comments: true
featured: true
---

A week or two ago I was discussing with a work colleague accessibility and they showed me a really cool Chrome extension named [ChromeLens](http://chromelens.xyz/). ChromeLens is a Chrome DevTools extension to develop for the visually impaired.

One of the fantastic features of [ChromeLens](http://chromelens.xyz/) is the tracker feature. [ChromeLens](http://chromelens.xyz/) Tracker is a blindness simulator that shows the pathway by which a blind user will go through when browsing your web page with a screen reader. You can check if your web page goes through a logical flow and that the important content is included for the screen reader to narrate. 

It's great because you can start a trace, tab through the application and you get a visual representation of the flow of your application.

![_config.yml]({{ site.baseurl }}/images/chrome-lens-flow.png)

Whilst this is a fantastic browser extension I am always looking at new approaches to automate things which I would need to do over and over again manually.

Today I started to look at how we could automate similar functionality to ChromeLens but using pure javascript to draw the flow, with the idea of then using visual testing to then take a screenshot of the page flow and see if the flow still is as expected. This would enable teams to start to automate visual testing of page flows for web applications!

Below is the JSFiddle code I created to draw the flow on the web page.
<script async src="//jsfiddle.net/11vlr/oeaf1mcb/2/embed/"></script>

![_config.yml]({{ site.baseurl }}/images/page-flow.png)

Using the [visual testing code](https://github.com/vivrichards600/AutomatedVisualTesting) example project I have made on GitHub the idea would be to use the WebDriver to inject the above javascript into a webpage to draw the flow, then take a snapshot and then do the visual comparison.

I have not updated the [visual testing code](https://github.com/vivrichards600/AutomatedVisualTesting) project yet with this example but wanted to share this idea as it is pretty cool!

As always any feedback and comments are welcome.