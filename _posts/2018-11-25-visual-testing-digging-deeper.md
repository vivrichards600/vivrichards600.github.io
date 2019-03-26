---
layout: post
title: Visual testing - digging deeper
description: 
headline: 
modified: 2018-11-06
category: Testing
tags: [accessibility testing, visual testing, usability, automation, d3, charts, pdf, documents, web testing]
imagefeature: 
mathjax: 
chart: 
comments: true
featured: true
---

Over the last 14+ months I've been very fortunate to be asked to speak all over the UK, Europe and in the USA about visual testing. The feedback on my sessions have been really positive but the questions at the end of the session are almost always about problems which may be faced when using visual testing to test a web application. 

Over the last two months I've come across a few other really cool ways which you can use visual testing to possibly start writing automated checks for things you wouldn't neceessarily think about writing checks for and so I thought I'd write a quick post to summarise these different ways.

## PDFs / Documents
In the majority of my talks ([you can find a link to some of the videos here](http://vivrichards.co.uk/events/)) I talk about document checking with visual testing.

One of the really great things I've used at my current employer is visual testing to check pdf documents. We use a 3rd party named [Aspose](http://www.aspose.com) (other products are available) which enables us to extract a specified page or all pages of documents into images. 

Within our tests we pass a pdf document to Aspose and covert the whole document or a specified page into an image or images and then run these through the image comparison checks. This allows us to compare documents very quickly. 

This can be really handy when dealing with documents in a foreign language for example or with documents which may have subtle hard to notice changes within it. 

## Charts
At my current employer we are creating a new chart framework using [D3](https://d3js.org/). 
When it came to start thinking about writing automated checks for the charts this became quite tricky. Of course you can write a check to assert some data, do an action to perhaps increase/decrease the data, and then check some data points in the chart are what you expect but this is a bit of a long winded process. 

Instead we decided to create a JavaScript function within our application which we were able to call at any point via the Selenium [WebDriver](https://www.seleniumhq.org/projects/webdriver/) executeScript method which when called set the data within the charts which were rendered to known data. This then allowed us to use visual testing to check that the custom chart framework was rendering as expected.

## Accessibility flow (tabability - is that a word??)
[I've recently written a short post on visual accessibility testing](http://vivrichards.co.uk/testing/automating-page-tab-flows-using-visual-testing-and-javascript) but wanted to quickly mention it here. Again by using the executeScript method within WebDriver you can inject some JavaScript to make the screen draw out a visual 'flow' so that you can see how the user would tab through your web application. This is really powerful and many people who talk about automating accessibility generally refer to checks which check the page markup rather than usability of a web application.

## Do you use visual testing some other way?

I'd love to hear from you if you use visual testing and use it for something other than what's listed above? 
