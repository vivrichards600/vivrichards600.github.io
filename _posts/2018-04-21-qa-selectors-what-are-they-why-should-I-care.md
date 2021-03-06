---
layout: post
title: Qa- selectors, what are they and why should you care?
description: 
headline: 
modified: 2018-04-21
category: Automation
tags: []
imagefeature: 
mathjax: 
chart: 
comments: true
featured: true
---

Over the past year as part of a talk on visual testing I've been presenting, I've talked a bit around writing easier to implement and maintain tests using qa-selectors. This seems to have gathered quite a bit of interest and positive feedback, and so I thought I'd write a very short blog post on what they are, why I think you should use them and how to start using them.

Typically when writing automated UI tests you have various options to find elements on a page to interact with. Ideally you'd locate an element by Id as these should always be unique, but if it's not available you'd then start looking at other ways to find elements by using things like Class Name, CSS Selector, Tag Name, Link Text or at the very worse case - XPath!!! The issue is that sometimes Id's change or aren't available, and when looking for an element by Class or Css Selector you may find that more than one element shares the same Class name for example.

Even if you manage to find an element by a unique Class name or some other selector and you create a test which works, what's stopping somebody from updating the webpage, changing the Id or Class name possibly and breaking your tests. Even worse, if you have more than one test using the same selector you now have many tests which would now break. Of course you could look to use something like the [page object pattern](https://martinfowler.com/bliki/PageObject.html) as talked about by Martin Fowler, but this still doesn't help your team make less breaking changes. Also your tests may be finding some elements by ID, some by CSS Selector and some using some other selector and so even if you update your tests and they now pass, they still may be a pain to maintain.

Using qa- selectors help to make your tests a lot cleaner, easier to maintain, help make it clear when elements are being relied on for automated UI tests - plus you can still use qa- selectors along with the page object pattern if you wish!

The idea is that for each element that you want to interact with using selenium web driver or your chosen UI tool/framework you give it a meaningful class name. So for example if you had a form with two buttons (submit and cancel), you give them both a qa- selector class name using a css selector.

The naming convention we tend to use is qa-{element-type}-{name}, so for example to give a save button a qa- selector we'd assign it a class name of :

```html
<input type="button" class="qa-button-save" value="Save">
```

Below is an example contact form with the html markup without qa- selectors along with html markup with qa- selectors.

![_config.yml]({{ site.baseurl }}/images/qa-selectors.png) 

Using the qa-selector now makes your UI automation tests cleaner, now everytime you want to find an element you won't need to think "do I need to use find by Id or CssSelector", you will always find by CssSelector and specify the qa- selector name! Now the next time somebody goes to make changes to the front end of the application and they see class names of "qa-" they should be aware that these elements are now being used for UI tests, and so they are less likely to make breaking changes. Perhaps they will see these and it will start a conversation rather than them just changing something which breaks your tests?

If your unhappy to add qa-selectors yourself, this is a perfect opportunity to break down barriers and pair up with a developer for example, talk through what you want to automate and share knowledge!

Hopefully the above will help you to create cleaner, easier to maintain tests with your team making less breaking changes.
