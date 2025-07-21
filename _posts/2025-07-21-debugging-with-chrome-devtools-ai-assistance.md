---
layout: post
title: Debugging with Chrome DevTools AI Assistance
description:
headline:
modified: 2025-07-21
category: DevTools
tags: [DevTools, AI, debugging, elements panel, chrome]
imagefeature:
mathjax:
chart:
comments: true
featured: true
---

In my [previous blog post](https://vivrichards.co.uk/devtools/devtools-ai-assistance-find-selectors-a-handy-assistant-not-replacement), I explored how Chrome DevTools’ AI assistant could help identify and understand selectors. This time, I wanted to try it out on something different - debugging.

On the [Sweet Shop basket page](https://sweetshop.vivrichards.co.uk/basket), I intentionally introduced a small bug. When a user adds one or more items to their basket, everything works fine - items appear as expected, and the total updates correctly. However, once shipping is selected, things start to go a bit… wobbly.
## Reproducing the Bug

I added 1 × Sherbet Discs to my basket, which totalled £0.95 as expected. Then I selected `Standard Shipping`, which should add £1.99 to the basket total.

Instead of seeing the expected combined total of £2.94, I saw: `NaN`

Yep. “Not a Number.”

## Asking Chrome DevTools AI assistance for Help

To dig in, I:

1. Right-clicked the Standard Shipping element on the page.
2. In the Elements panel, I right-clicked the selected element and clicked `Ask AI`.
3. I asked:

>When this element is clicked it should add the total to the shipping cost but it's showing `NaN`. I can see in the elements panel that the element also has an `onclick` method called `getCartDetails()`,

The AI responded with a helpful explanation:

>"NaN (Not a Number) usually results from an operation where a value that cannot be represented as a number is involved in a mathematical calculation…"

It suggested I look for the `getCartDetails()` function, since it was being called via the `onclick` attribute, and advised checking how the `subTotal` and `shippingCost` were being calculated.

## Locating the JavaScript Function

Next, I asked:

>can you help locate where the `getCartDetails` method would be?

The AI assistant guided me to:

1. Open the Sources panel in DevTools.
2. Use "Search in all files" from the file tree.
3. Paste in `getCartDetails` to locate the function definition.

Following its advice, I found the `getCartDetails()` function within a file named `custom.js`. I copied the entire `getCartDetails()` function and pasted it into the AI assistant for review.

## Spotting the Issue

The assistant pointed to this line as the likely culprit:

```javascript
totalWithShipping = subTotal + shippingCost;
```

It explained:

>"shippingCost is obtained from `document.getElementById('exampleRadios2').value`. The `.value` property always returns a string. When you use the `+` operator with a string and a number, JavaScript concatenates them instead of adding."

So in this case, `0.95 + "1.99"` could result in `"0.951.99"`, or worse, something that breaks the formatter and produces `NaN`.

## The Suggested Fix

The AI recommended changing the line to:
```javascript
totalWithShipping = subTotal + parseFloat(shippingCost);
```

To confirm, I tested both versions directly in the browser console using these values:
```javascript
let subTotal = 0.95;
let shippingCost = "1.99";

// Broken version
let totalWithShipping = subTotal + shippingCost; // Outputs: "0.951.99"

// Fixed version
totalWithShipping = subTotal + parseFloat(shippingCost); // Outputs: 2.94
```

Success!

## Let it support your debugging, not lead it

While it’s not a silver bullet, Chrome’s AI assistance can be an incredibly useful pairing partner, not just for developers, but for testers too. As a tester, I often use DevTools to investigate unexpected UI behaviour, review DOM elements, or debug client-side logic. Having an AI-powered assistant to help reason through issues or suggest where to look next is like having an extra set of eyes when you're exploring or diagnosing tricky bugs.

Using the AI assistant and testing its output was a fast and informative way to both reproduce and resolve the issue. The assistant not only provided a working fix, but also explained the reasoning behind it clearly.

You can [read more about the Chrome DevTools AI assistance here](https://developer.chrome.com/docs/devtools/ai-assistance).
