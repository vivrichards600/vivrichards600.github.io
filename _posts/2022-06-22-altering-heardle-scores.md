---
layout: post
title: Exploring Heardle - achieving a perfect score
description:
headline:
modified: 2022-06-22
category: Automation
tags: [heardle, exploratory testing]
imagefeature:
mathjax:
chart:
comments: true
featured: true
---

Following on from my previous two blog posts that explored [how to automate guessing Heardle](2022-06-18-gaming-heardle-the-art-of-keeping-things-simple.md) and [listening to a previous or upcoming Heardle](2022-06-20-listening-to-previous-days-or-upcoming-heardle.md), in this post I explore how to alter Heardle to achieve a perfect score.


> **Spoiler Alert**: The following information explains how to alter your daily Heardle stats.  

The aim of this post isn't to encourage cheating at the game. Instead, I want to share some ideas about exploring an application and how it can be manipulated to behave in a way that isn't how the developer(s) of the game intended.

Sometimes, no matter how long you spend listening to the first second of a Heardle, it just isn't enough. It can be so frustrating. Yesterday I wasn't 100% on the Heardle for the day and so decided to click the `Skip` button to hear another second of it. After the additional second played, I got it. Doh! I should have known this one, and now I've lost my perfect score for the day...

As a reminder of your guesses, Heardle provides its users with an overview of their scores. Within the stats window, you can see the number of Heardles you've guessed, and they get grouped by the number of attempts it took you to guess. My daily Heardle of the day was now showing two attempts.

![heardle.app stats]({{ site.baseurl }}/images/heardle-stats.png)

This got me thinking, is it possible to change a Heardle score? What if we could hide the fact we had to skip when guessing the Heardle to get a perfect score for the day?

When I explore a web application, one of the tools I really love using is DevTools. DevTools contains many tools that can help you in your day-to-day testing of web applications and are built into the web browser. I’m not going to talk much about how to use DevTools in this post, but if you’d like to learn more about DevTools and how to use it to generate new test ideas, why not check out my course over on the Ministry of Testing site.

[![A software testers guide to Chrome DevTools course]({{ site.baseurl }}/images/course_banner.png)](https://www.ministryoftesting.com/dojo/courses/a-software-tester-s-guide-to-chrome-devtools)

To start on my mission of a perfect score, with [Heardle](https://heardle.app) opened within my Chrome web browser I right-clicked and inspected the page. One of the things I often do when I see that a web application is storing information on my usage is that I like to go to the [Application panel within DevTools](https://developer.chrome.com/docs/devtools/#application). Within this panel, there are a number of different things you can look at. When I use this panel I like to look at the Cookies and Local Storage. 

When inspecting the Heardle page and looking at the Cookies panel there were some entries for Heardle. After a closer inspection, sadly only Google Analytic information was being stored here for Heardle. Next, I headed over to the Local Storage section.

The Local Storage API is used by some web applications as a way to store, retrieve, and track changes to user data. Within this panel, there were two entries for Heardle. One called `firstTime`, with a value of `false`, and the other called `userStats` which contained some interesting-looking JSON. 

![Viewing local storage for Heardle]({{ site.baseurl }}/images/viewing-local-storage.png)

I altered the `firstTime` value and reloaded the page. The behaviour changed as if it was the very first time I had opened Heardle with a how-to-play splash screen being displayed. Whilst this showed the splash screen, my stats were unchanged.

Next, I looked at the `userStats` JSON value. There was lots of interesting information:

<pre>
[
  {
    "id": 116,
    "guessList": [
      {
        "answer": "",
        "isCorrect": false,
        "isSkipped": true,
        "isArtist": false,
        "playCount": 1
      },
      {
        "answer": "The Foundations - Build Me Up Buttercup",
        "isCorrect": true,
        "isSkipped": false,
        "isArtist": false,
        "playCount": 1
      }
    ],
    "hasFinished": true,
    "hasStarted": true,
    "img": "https://i1.sndcdn.com/artworks-hnz9Jtey8tXv-0-large.jpg",
    "gotCorrect": true,
    "score": 2
  }
]
</pre>

From looking through the JSON value there were some interesting things being stored. A `guessList` which seemed to keep track of the number of attempts and also because I had got the Heardle on my second attempt, there were some values to indicate I'd finished the Heardle (`"hasFinished": true`), got the answer correct (`"gotCorrect": true`) and that it took me two guesses (`"score": 2`)

I wanted to start modifying the JSON value, in particular the `guessList`. I copied the entire `userStats` JSON value and pasted it into [a free online JSON formatter](https://jsonformatter.org/json-pretty-print) so that I could easily view and modify the structure. Next, using the online editor I removed the contents within `[` `]` for the `guessList`. I also changed the `score` value to `1`. Then I clicked on the `Make Pretty` button on the online formatter, copied the formatted JSON and pasted it into the Local Storage, over-writing the `userStats` value. 

I reloaded the webpage and clicked on my stats. A perfect score! 

![heardle.app altering score]({{ site.baseurl }}/images/heardle-alter-score.gif)

When exploring, I also purposely removed all of my Local Storage to see what other things we might want to do. One scenario was getting to a point where you use all your skips and so you run out of turns and the Heardle is revealed.

In this scenario, you could modify the `userStats` JSON value and just remove the days Heardle. You can do this by amending the `guessList`. To do this you would remove the JSON starting with `{ "id:` (make sure you remove the correct Heardle) down to the closing bracket `}` just after the `"score":` value for the Heardle.

Now you could listen to the song again, put in the correct song and get the correct answer in one guess ;-). 

