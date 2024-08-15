---
layout: post
title: Using DevTools to add a custom Video in Google Meet
description:
headline:
modified: 2024-08-15
category: DevTools
tags: [DevTools, Google meet, JavaScript, Tools]
imagefeature:
mathjax:
chart:
comments: true
featured: true
---

With the growth of remote work, tools like Google Meet are constantly evolving to enhance the virtual meeting experience. Among its features, Google Meet offers [visual filters for backgrounds and faces](https://support.google.com/meet/answer/10058482?hl=en-GB&co=GENIE.Platform%3DAndroid), enabling users to blur their surroundings, select from preset images or videos, or even upload custom images.

These features are often used to bring a bit of fun to online meetings and team catch-ups. However, while you can upload custom images, it’s puzzling that there doesn’t seem to be an option to upload custom background videos—or is there?

If you've read some of my previous blog posts, you know how much I enjoy using Chrome's DevTools. In one post, I discussed [how DevTools can be used to bypass client-side validation](https://vivrichards.co.uk/testing/removing-required-field-validation). While playing around within Google Meet, I noticed that when selecting a custom background image, the DOM ([Document Object Model](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model))  could be modified to allow the addition of custom video backgrounds. This discovery opens up exciting new ways for making your Google Meets a little more interesting.

### Adding your own background videos to google meet

1. Start a new or join an existing [Google Meet](https://meet.google.com/landing)
2. Click on Apply visual effects
3. Open DevTools within Chrome :
    * Windows: `CTRL+SHIFT+J` OR `F12`
    * Mac: `Command+Option+J`
    * You can also open through the wrench menu (Tools > JavaScript Console)
4. Paste the following snippet into the console tab and press `Enter` on your keyboard to execute the snippet on the web page you are currently viewing

```javascript
// Find the file input to upload a new background
const inputElement = document.querySelector('input[type="file"]');

// Append 'video/mp4' to the 'accept' attribute if the element is found
if (inputElement) {
  inputElement.setAttribute('accept', inputElement.getAttribute('accept') + ', video/mp4');
}
```

The above snippet find's the file upload input and alters the `accept` attribute to allow mp4 videos to be chosen in the popup window when selecting a file.

![Executing the file upload button in Google Meet using the console within DevTools]({{ site.baseurl }}/images/devtools-modify-element-console.png)

Now when you choose to add a custom background to use in Google Meet, you will now be able to add your own custom video.



