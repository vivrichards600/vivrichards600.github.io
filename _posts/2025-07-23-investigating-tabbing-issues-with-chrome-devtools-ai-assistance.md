---
layout: post
title: Investigating Tabbing Issues with Chrome DevTools AI Assistance
description:
headline:
modified: 2025-07-23
category: DevTools
tags: [DevTools, AI, accessibility, chrome]
imagefeature:
mathjax:
chart:
comments: true
featured: true
---

In my last couple of posts, I explored how the Chrome DevTools AI assistance can help identify DOM selectors and assist with debugging client-side issues.

* [Using AI Assistance in Chrome DevTools to Find Selectors](https://vivrichards.co.uk/devtools/devtools-ai-assistance-find-selectors-a-handy-assistant-not-replacement)
* [Debugging with Chrome DevTools AI Assistance](https://vivrichards.co.uk/devtools/debugging-with-chrome-devtools-ai-assistance)

In this post, I’m turning my attention to accessibility, how the Chrome DevTools AI assistance can help identify and correct tabbing issues on a page.

##  Setting Up the Problem
I deliberately introduced a tabbing issue on the [Sweet Shop login page](https://sweetshop.vivrichards.co.uk/login). The goal was to simulate a real accessibility problem so others could practise spotting and debugging it - whether they’re testing for usability, compliance, or general keyboard navigation.

To confirm the issue, I used the keyboard to tab through the page. As expected, the tab order didn't follow the logical flow of the form. The focus skipped around, which would be confusing for users relying on keyboard navigation or assistive technologies.

## Asking the AI Assistance
To start investigating, I opened DevTools, selected the `<form>` element containing the input fields (since the visual tab order felt off), and clicked **“Ask AI”**.

I asked:

>When I tab within this page, the tab order is not right, why is this?

The assistant analysed the DOM and responded with:

>The most likely reason for the unexpected tabbing order is the use of the `tabindex` attribute on the input elements.

It noted:

* The email input (`exampleInputEmail`) had `tabindex="1"`.
* The password input (`exampleInputPassword`) had `tabindex="0"`.
* Other elements had no explicit tabindex set.

Then it gave a solid explanation of how browsers handle tabbing:

>Elements with a positive `tabindex` (1 or higher) are focused first, in numerical order. After those, elements with `tabindex="0"` or no `tabindex` are focused in source order.

So in this case, the browser was giving focus to the email input before the password field, even if the source order suggested otherwise.

## AI Assistance Modifying the Page
After its analysis, the assistant asked me:

>Would you like me to remove the `tabindex` attributes from the inputs?

I replied:

>Yes, remove the `tabindex` attributes.

The AI initially tried to apply a CSS method, but quickly corrected itself acknowledging that `tabindex` is an HTML attribute and should be removed using JavaScript’s `removeAttribute()` method.

It then removed the attributes from both the email and password fields.

## Verifying the Change
With the fix automatically applied by the AI assistance, I re-tested the tab order. This time, the focus followed the expected sequence based on the form’s source order with no unexpected skips or jumps.

I also inspected the DOM to verify that the AI assistance had removed the `tabindex` attributes as it said it had.

## Use it to assist, not to automate your thinking
Once again, Chrome’s AI assistance helped explain what was happening, offered a clear diagnosis, and followed through with a suggested fix as well as automatically applying it for me - all within DevTools. It even adjusted its approach when the first method wasn't appropriate.

As a tester, I found this particularly useful for accessibility exploration. Tools like this help surface DOM level behaviour that might otherwise go unnoticed, but they’re most effective when paired with critical thinking and validation.

You can [read more about the Chrome DevTools AI assistance here](https://developer.chrome.com/docs/devtools/ai-assistance).
