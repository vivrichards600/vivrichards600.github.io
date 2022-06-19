---
layout: post
title: Automating Heardle - The art of keeping things simple
description:
headline:
modified: 2022-06-18
category: Automation
tags: [automation, heardle, exploratory testing]
imagefeature:
mathjax:
chart:
comments: true
featured: true
---

My whole family love to play [Heardle](https://heardle.app). If you haven't heard of it before, Heardle is a game where each day you have to listen to the intro of a song, then guess the correct artist & title. It's a really fun game that we all enjoy playing on our phones but it got me thinking, is this game something that I could automate to correctly guess the Heardle each day?

> **Spoiler Alert**: The following information explains how to solve the daily Heardle in a way that wasn't intended by the games author(s).

![heardle.app]({{ site.baseurl }}/images/heardle-app.png)


When I first started to think about this, my mind raced through various ways I might approach this. The biggest challenge I find often with things like this, is me. I have to try and rein it in, there are so many ways to do things, and I love to try new things and often get carried away. I am aware of various services for example that could guess a song artist and title from playing a song, there are also many browser plugins, APIs etc. which could assist with guessing a song.

I fired up my laptop and opened my IDE and started to write a test, I knew I'd want to open a Chrome browser window and so did so in my test and then navigated to [https://www.heardle.app/](https://www.heardle.app/). The next thing was to try and work out the best way to capture the audio from Heardle.

I decided to inspect the page and take a look at the play button on the site. Immediately I found a selector to interact with the Play button and implemented it within my test. Next, now the Heardle was playing, I wanted to try and inspect the page again and see what information was displayed for me to try and obtain the Heardle artist and title somehow. There wasn't an awful lot to be seen. A few divs, an SVG for the play button. Next, I looked at the Event Listeners for the button and clicked on the script for the element. The developer for this fun app made JavaScript very difficult to read.

I proceeded for quite a while to browse chrome extensions and see if any could fit the bill for what I needed. The initial idea would be to add the chrome extension into the browser of the test, capture the audio, grab the guessed song from the extension and then use sendkeys within selenium to input an answer into the Heardle site.

After way too much time spent, I went back to explore the application within DevTools. Within the Network tab, I looked around to see what requests were being made by the app. 30 minutes later from exploring I stumbled upon an interesting network request being made to Soundcloud. The URL interestingly also contained both the artist and song title within the url. Eureka!

Now at this point, I’d like to state I automated all the things and all was working as hoped… not quite. I knew the network tab surfaced a request which contained the artist and title, but instead of keeping it simple, I started using selenium in my test to look at the network requests being made in the browser using DevTools. My thoughts were to find the network requests, extract the artist and/or title, and submit it via Heardle.

A very long story short, I started to go down a rabbit hole and things started to become very complex, quickly. I decided to take a short break away from the computer as I became frustrated with how the challenge was going. 

I came back and tried to look at the problem afresh. I knew there was a request being made to Soundcloud and this request always had the artist and URL so what could I do? I started to explore the application more.

As I inspected the page I found a div with a hidden class name, interesting! It was this div that contained an iframe with the same URL that I had noticed within the network tab being called. If only I had just searched for the same URL within the Elements tab of DevTools sooner I’d have found the answer, and it was a lot simpler than I thought.

Now it was easy, to navigate to the Heardle page, find the hidden element, obtain the song title from the hidden fields URL, submit it and that’s it. There were a few small gotchas. Sometimes, the title for the song can be very short or contain -1 for example within the URL. It's not perfect but to ensure the code worked as expected I had to do a quick and dirty string replace to remove the -1 and added some simple logic to only get the first 10 characters of the title if it was greater than 10 characters as some title have for example Remastered 2014 which doesn't come up within the auto complete.

![heardle solution]({{ site.baseurl }}/images/heardle-solution.gif)

After trying this in my selenium test, it worked perfectly ([My simplistic solution can be found here](https://gist.github.com/vivrichards600/8a42aed3ca7ab7c4f2219952de067f3e)). Of course there is lots of refactoring that could and should be done, but as this was just to a bit of fun, I'm not too concerned.

This challenge was so fun, and the solution ended up being so simple. It reminded me of a few things. Sometimes you really need to try and keep things simple. Try to reign it in and not over-engineer the solution. Don't jump in with both feet just trying to write some automation and get carried away. 
Explore the application, and understand it.  

More often than not, the best solutions are the simplest ones.


