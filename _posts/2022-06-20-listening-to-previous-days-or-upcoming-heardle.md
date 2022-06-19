---
layout: post
title: Exploring Heardle - Listening to missed or upcoming days
description:
headline:
modified: 2022-06-18
category: Testing
tags: [heardle, exploratory testing]
imagefeature:
mathjax:
chart:
comments: true
featured: true
---

As I mentioned in a [previous post](2022-06-18-gaming-heardle-the-art-of-keeping-things-simple.md), my whole family and I, love to play [Heardle](https://heardle.app). Whilst I try to listen to the daily Heardle, sometimes I forget and so miss the chance. The game currently also doesn't have a way to revisit a previous Heardle.

> **Spoiler Alert**: The following information explains how to use Heardle in a way that wasn't intended by the games author(s).

This post isn't being written to encourage cheating at the game. Instead, I wanted to share some ideas around exploring an application and showing how it could be manipulated to behave in a way that wasn't quite how the developer(s) intended.

![heardle.app]({{ site.baseurl }}/images/heardle-app.png)

When software testing and exploring an application. There are many [heurists you might wish to use](https://www.ministryoftesting.com/dojo/lessons/test-heuristics-cheat-sheet). There are multiple definitions of using a Heuristic, here's one from the Cambridge Dictionary:

>“A method of learning or solving problems that allow people to discover things themselves and learn from their own experiences.” – Cambridge Dictionary

One thing we know about the [Heardle.app]([Heardle](https://heardle.app)) is that a new song is released each day. What if we could alter the day and then go back and listen to a previous days Heardle? 

By altering the date on my computer and then reloading the page, guess what happens. Why not try it yourself and see ;-) ?

![heardle.app altering the date]({{ site.baseurl }}/images/heardle-alter-date.gif)

Now we can revisit old Heardle's we might have missed. Not only that, we can change the date to a future one. Now you can guess the next days Heardle before it's meant to be available on the game. 

In my [previous post](2022-06-18-gaming-heardle-the-art-of-keeping-things-simple.md) I showed how you could automatically guess a Heardle. Now we could automatically guess any previous or future Heardle.

![Change date and automatically guessing the Heardle]({{ site.baseurl }}/images/headle-date-change-automated-guess.gif)

Have fun and happy exploring!


 

