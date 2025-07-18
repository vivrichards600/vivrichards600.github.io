---
layout: post
title: Using AI assistance in Chrome DevTools - A Handy Assistant, Not a Replacement
description:
headline:
modified: 2025-07-18
category: DevTools
tags: [DevTools, AI, console panel, elements panel, chrome]
imagefeature:
mathjax:
chart:
comments: true
featured: true
---


I recently came across an interesting [post on the Ministry of Testing Club](https://club.ministryoftesting.com/t/useful-tip-for-web-automation-inspecting-web-elements-understanding-dom-using-ai/85826/) highlighting the AI assistance built into Chrome DevTools. It showcased how someone had used the feature to help identify a selector for a web element – and impressively, the AI gave them exactly what they needed.

Naturally, I had to give it a go myself.

## Testing the Chrome DevTools AI assistance

I fired up my [Sweet Shop site](https://sweetshop.vivrichards.co.uk/) and navigated to [the basket page](https://sweetshop.vivrichards.co.uk/basket). There, I have a couple of form fields – First name and Last name – both implemented using similar HTML:

```html
<input type="text" class="form-control" id="name" ... >
```

Yep, you spotted it – both inputs have the same ID. Not ideal, but for the sake of the experiment, it worked a treat.

When I highlighted the First name field and asked the DevTools AI assistance:

>I need to find this element within my Scala code. I am writing UI journey tests with Selenium.

It returned a sensible response, recommending:

```scala
val nameInput = driver.findElement(By.id("name"))
```

On the surface, this looks fine. But here’s where it gets interesting. In the console, `document.getElementById('name')` returns the first matching element (First name). However, when searching with the XPath `//input[@id='name']` in the Elements panel, Chrome showed 2 results – First name and Last name.

This is a classic example of how AI might give you an answer that looks right but doesn’t consider the underlying context. In this case, duplicate IDs – something we shouldn’t really be doing, as IDs are meant to be unique.

To take things further, I asked it:

>Give me the best selector to use for this element given it shares the same ID and class name as another on the page. I want to select the second element (Last Name).

To its credit, it came back with several options and even explained the trade-offs. One such selector was:

```css
.col-md-6.mb-3:nth-of-type(2) input#name.form-control
```

This one, when tested in the Elements panel, returned just the Last name field.

## Use it to assist, not to automate your thinking

The AI assistance in DevTools is a handy tool – it can help break down what’s going on, point you in the right direction, and even explain why something may or may not work. But it shouldn't be followed blindly.

You still need to test, validate, and understand what it’s giving you – otherwise, there’s a risk of blindly trusting suggestions and gradually downskilling. Think of it as a co-pilot – helpful, but you're still flying the plane.

You can [read more about the Chrome DevTools AI assistance here](https://developer.chrome.com/docs/devtools/ai-assistance).
