---
layout: post
title: Thinking outside the testing box
description: 
headline: 
modified: 2018-08-05
category: Testing
tags: [testing, software, development, automation]
imagefeature: 
mathjax: 
chart: 
comments: true
featured: true
---

Recently I started to think about how teams test and how quite often it's difficult to think about testing as a bigger picture when you aren't aware what that bigger picture is.

Quite often people tend to stick to what they know and so unless they are aware of other things they could be doing, then they aren't going to start thinking about doing it.

To give an example, I've worked with people who have always tended to stick to manual happy path testing and then writing UI (selenium) automated tests to try and save some time and gain some confidence in the software that they are shipping every few weeks. The problem is that these types of tests are slow to implement, expensive to implement and to maintain, plus there are lots of different ways which these individuals and teams could and should be testing this software! 

Imagine a shopping cart, a user can visit your website, add some items, if they buy more than one of the same item they get money off, and finally you get a final balance which you can then click pay to go to the checkout. 

The number of times I've seen testers write UI tests to test all of the logic of the shopping cart is unbelieveable. Not only is this absolutely crazy, but it's a waste of time - if the tester had conversations within their team they could have looked to add these tests further down the stack at the unit and integration levels. Whilst testers often have less technical skills than developers, they often have more business knowledge than the developers and so developers and testers should be working together to add as much value as they can, together! 

It can be difficult sometimes to see where you can add value or to identify opportunities to pair together, but using things like WIP (Work in Progress) limits can help, look for opportunities to pair up, pairing can be a fantastic way to rubber duck for the developer and also give you as a tester a real overview of how the new feature for example has been implemented to start help you generate ideas on how you may try to test the new feature.

I believe often it can be a cultural thing, companies, teams and people work in a certain way and people get used to that way of working. I also believe that quite often there are people who want to push boundaries, do the best job they can, but it's difficult sometimes if you haven't been exposed to different ways of working or other ways to possibly add value as a tester.

One way we've tried to do this where I work is to run an exercise where we got the test team together to start to think about testing on the applcations we work with. The testers were asked to break in to small teams and given three different colour post it notes (green, yellow red). On the green post it's testers were asked to write down testing they think they always do, yellow what they sometimes do and red what they think they don't do. For example, some of the types of testing which were written down were Unit, integration, stress, performance, localisation, api, accessibility visual, database, manual testing.

Next a [test pyramid](https://martinfowler.com/articles/practical-test-pyramid.html) was drawn on to the board. Here testers were asked to stick the post it notes on to the board where they believed that type of testing belonged. This was quite eye opening, the majority of green post it notes were at the top of the pyramid, showing that the majority of testing carried out by the teams was where we were getting the slowest feedback, from the tests which took the longest to implement and maintain. The other quite interesting thing was that some of the post it notes were actually stuck next to levels where the test types didn't belong, for example, a visual testing post it note was stuck next to the integration level and note the UI level.

The exercise I felt was also great beccause it helped to identify knowledge gaps within the team, helping us to start talking about other levels/types of testing teams and individuals hadn't previously thought about. An outcome from the exercise was an idea to start to look at having testers as SMEs (Subject Matter Experts) in different areas of testing so that we can start to start thinking about the bigger picture and have people highly skilled in the various areas of testing.

Whilst we cannot all be experts in every aspect of testing, if we are aware of different types of testing and are able to identify when we may benefit from changing our approach, then we can reach out to others to get help if we lack experience or knowledge in that area. 

Time can often be an issue to test in other ways but as part of scrum ceremonies (3 amigos, refinement and planning) we have the opportunity as part of the definition of done, to get time in order to test ‘enough’ to give us the confidence in the software that is being shipped. If you find you are not given the time then this is a
bigger problem which should be taken up with your scrum master or team.

It's always good to reflect and think what can I as an individual or we as a team do better. How can you look to add more value sooner? What can you do as a team, to work smarter in order to deliver software with more confidence.

