---
layout: post
title: End-to-end testing a Chrome extension using Puppeteer
description:
headline:
modified: 2023-01-06
category: Automation
tags: [automation, chrome, extension, puppeteer, testing, manifest v3]
imagefeature:
mathjax:
chart:
comments: true
featured: true
---

Toward the end of last year, I spent time developing a couple of Chrome browser extensions. During the development of these one of the things that I found a bit of a pain was testing them.

When testing the extensions I used [Jest](https://jestjs.io/) to help implement unit and integration tests. Alongside this, I also used [Jest Chrome](https://github.com/extend-chrome/jest-chrome) to mock some of the Chrome APIs used in the Chrome extensions.

As well as having the above tests in place, when developing an extension, often you'll want to re-load the unpacked extension in your browser, interact with it or perform an action and ensure it's working as expected. If something is wrong often it's not immediately apparent. Sometimes it will require you to try to reload the extension or even interact with it or a page before you are made aware a problem has occurred. This is also not helped by the fact that many errors for example that are thrown are often displayed in the Chrome DevTool console for one of your scripts and so an issue might not be immediately obvious.

To combat this frustration the one thing I wanted to conduct was end-to-end testing for these extensions.

One option you could consider is to implement a task runner using something like [Grunt](https://gruntjs.com/) to watch for any file changes and then reload your Chrome extension as you develop it but depending on the type of browser extension you're developing you'd still want to interact with it to ensure it's behaving correctly.

This is where [Puppeteer](https://pptr.dev/) comes in.

## A simple Chrome extension to test
To make things as simple as possible to follow, in this blog post we will use Puppeteer to test the [Chrome ‘Hello Extensions’ extension](https://developer.chrome.com/docs/extensions/mv3/getstarted/development-basics/). The above guide explains how to create a simple Chrome extension that displays an extension with a 'Hi' icon in the extensions bar. Once the ‘Hi’ icon is clicked, the text `Hello Extensions` is then displayed within the popup.

If you’d like to create the extension to try for yourself but prefer to not have to follow the above guide, [the code for this 'Hello Extensions' Chrome extension can be found here](https://github.com/vivrichards600/puppeteer-extension-example/tree/Hello-Extensions).

## End-to-end testing using Puppeteer
We won’t go into the ins and outs of [Puppeteer](https://pptr.dev/) and coding best practices in this post but instead will briefly look at [a simple Puppeteer end-to-end test that has been created for this blog post that tests the ‘Hello Extensions’ Chrome extension](https://github.com/vivrichards600/puppeteer-extension-example/blob/Puppeteer/hello-extensions.test.js).
A thing to note is that in order for us to write and execute a Puppeteer test we need to make a few changes to our extension as well as add a couple of things.

All of the code for the Chrome `Hello Extensions` browser extension and the Puppeteer end-to-end test code can be found here (https://github.com/vivrichards600/puppeteer-extension-example).

### package.json
In order to use Jest and Puppeteer within our test a new [package.json](https://github.com/vivrichards600/puppeteer-extension-example/blob/Puppeteer/package.json) file was added to specify our test will use jest as well as specifying dependencies on jest and jest-puppeteer versions to be used.

### background.js
In the end-to-end test the way that we are able to find the extensions url to navigate to is via a `service_worker`. In order to use a `service_worker` one needs to exist and be specified. To get this to work an empty [background.js](https://github.com/vivrichards600/puppeteer-extension-example/blob/Puppeteer/background.js) file was added to the project.

### Manifest.json
Following on from adding the `background.js` file in order to make use of the `service_worker` the [manifest.json](https://github.com/vivrichards600/puppeteer-extension-example/blob/Puppeteer/Manifest.json#L10-L12) was modified to introduce a `service_worker` and reference the newly created  [background.js](https://github.com/vivrichards600/puppeteer-extension-example/blob/Puppeteer/background.js) file.

### hello-extensions.test.js
Finally, a new [hello-extensions.test.js](https://github.com/vivrichards600/puppeteer-extension-example/blob/Puppeteer/hello-extensions.test.js) test file was added for the new end-to-end test.

Let’s take a look at what this test is doing.

```
const puppeteer = require('puppeteer');
let browser, page;
```
Here we specify that we require Puppeteer as this will be used for our test. We also specify two variables `browser` and `page`. The browser variable is used for the Chrome browser we will use. The page variable is the popup page we will navigate to and assert text.

```
const puppeteerArgs = [
    `--disable-extensions-except=${__dirname}`,
    `--load-extension=${__dirname}`,
    '--disable-features=DialMediaRouteProvider',
];
```
`puppeteerArgs` are separated out here to try and simplify the code. These arguments are specific to Puppeteer and passed to the browser when we launch it. Some of these args might seem obvious in their intention whereas others not so.

`--load-extension` and `--disable-extensions-except` is used to ensure our browser opens with only our extension loaded. `--disable-features=DialMediaRouteProvider` disables a popup that displays when the tests run that asks "Do you want the application “Chromium.app” to accept incoming network connections?"

```
describe('Hello Extensions', () => {

    beforeEach(async function () {
        browser = await puppeteer.launch({
            headless: false,
            slowMo: 200,
            args: puppeteerArgs
        });
        [page] = await browser.pages();
    });

    afterEach(() => browser.close());
```
Here we use a `describe` block. These are usually used to help organise test cases in logical groups of tests. We also make use of `beforeEach` which enables us to do something before each test in this file runs. In our test, we specify that we’d like a browser to launch. Upon launch, we specify `headless: false`. Puppeteer will not load extensions in headless mode, so we set this to false. `slowMo` is useful for debugging and slowing things down to watch the test run. `args` are those we specified above to only add our extension to the new browser window that’s launched and hide an annoying popup. The `[page]` variable is set to any pages launched as part of the browser. After each test is finished we use `afterEach` to ensure the browser is closed after each test.

```
    it('displays popup', (async () => {
        const targets = await browser.targets();
        const extensionTarget = targets.find(target => target.type() === 'service_worker');
        const partialExtensionUrl = extensionTarget.url() || '';
        const [, , extensionId] = partialExtensionUrl.split('/');

        const extensionUrl = `chrome-extension://${extensionId}/popup/hello.html`;

        await page.goto(extensionUrl, {waitUntil: ['domcontentloaded', "networkidle2"]});

        const popupHeading = await page.$eval('h1', (e => e.innerText));
        expect(popupHeading).toEqual('Hello Extensions');

    }));

});
```

When initially thinking about testing a Chrome extension end-to-end you might think the way you’d do this in a end-to-end test might be to load an extension, click on the icon in the test and assert something. This isn’t something that can be done in this way and so instead a way around this is to work out the Chrome extension id and then navigate to the popup page.

In the above code, using the `service_worker` we are able to find the extension id, which will allow us to load the extension in a new tab by referencing the chrome-extension:// namespace to access the extension popup. The path to the popup is set within `extensionUrl`.

Once we know the path to the popup we go to it. The `waitUtil` ensures we wait until the page is loaded before doing any assertions.

Finally, we specify that we want to obtain the `innerText` of an element on the popup page for a `h1` element. We then check that that text matched `Hello Extensions`.

### Running the test
Finally, to run the test we run `npm test`


![End-to-end testing 'Hello Extensions Chrome extension using Puppeteer']({{ site.baseurl }}/images/hello-extensions-puppeteer.gif)]

If you would like to try this for yourself, all of the code for the Chrome `Hello Extensions` browser extension and the Puppeteer end-to-end test code can be found here (https://github.com/vivrichards600/puppeteer-extension-example/tree/Puppeteer)




 