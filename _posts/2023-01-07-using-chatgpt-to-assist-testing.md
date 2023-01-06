---
layout: post
title: Using ChatGPT to assist testing 
description:
headline:
modified: 2023-01-06
category: AI
tags: [ai, chatgpt, testing, cucumber, gherkin, test data, study buddy, how to, tutorials]
imagefeature:
mathjax:
chart:
comments: true
featured: true
---

Back in November [ChatGPT](https://chat.openai.com/chat) was launched.

> ChatGPT is a chatbot launched by OpenAI in November 2022. It is built on top of OpenAI's GPT-3.5 family of large language models, and is fine-tuned with both supervised and reinforcement learning techniques.

Over the past few weeks, lots of people over social media have shared some really cool ways they have been using it to generate articles, find out information and even help generate code.

When I first saw all the hype about it I'll be honest, I thought it was pretty cool, but I couldn't at the time think of any ways that it might immediately benefit myself. 4 weeks later I revisited ChatGPT and discovered some really cool things that might be useful to assist software testing.

# Create Cucumber scenarios
I assumed ChatGPT would be able to write Cucumber scenarios but was curious in the style that it might use to write it.

I wanteed to see how ChatGPT would write Cucumber scenarios to test [the HMRC Government Gateway page](https://www.access.service.gov.uk/login/signin/creds), and so I asked: `cucumber example to login to hmrc portal`

```
Here is an example of how you could write a Cucumber test to log in to the HMRC portal:

Feature: Login to HMRC portal
As a user
I want to be able to log in to the HMRC portal
So that I can access my account information and perform actions on the site Scenario: Successful login

Given I am on the HMRC login page
When I enter my username and password
And I click the login button
Then I should be logged in to the HMRC portal

Scenario: Unsuccessful login
Given I am on the HMRC login page
When I enter my username and an incorrect password
And I click the login button
Then I should see an error message

This Cucumber test is written in the Gherkin language, which uses natural language phrases to describe the steps in the test. In this example, the first scenario tests for a successful login, and the second scenario tests for an unsuccessful login
```

Whilst the above is pretty good, the generated scenarios were written in an imperative style. To try and get it to [write better Gherkin](https://cucumber.io/docs/bdd/better-gherkin/) I then asked it: `write a cucumber example to login to hmrc portal in a declarative style`

```
Here is an example of how you could write a Cucumber test to log in to the HMRC portal in a declarative style:

Feature: Login to HMRC portal 
In order to access my account information and perform actions on the site 
As a user 
I want to be able to log in to the HMRC portal 

Scenario: Successful login 
Given I am on the HMRC login page 
When I enter my valid credentials 
And I click the login button 
Then I should be logged in to the HMRC portal 

Scenario: Unsuccessful login 
Given I am on the HMRC login page 
When I enter my valid username and an invalid password 
And I click the login button 
Then I should see an error message 

In this example, the first scenario tests for a successful login, and the second scenario tests for an unsuccessful login. The steps are written in a declarative style, using simple and straightforward language to describe the actions being performed.
```

The above whilst the Gherkin was written much better it could still be improved a little but created a great starting point to create some scenarios to help focus discussions.

Something to note with ChatGPT is it responds based on how it's been trained. So for example if it's been trained on public Github repositories you'll tend to get whatever style is prevalent by default although the beauty of ChatGPT is you can iterate on the answers.

## Create test data
Sometimes you might need to quickly generate some test data. Well ChatGPT can be really useful for this: `generate an array of 10 users consisting of firstname, lastname and date of birth in json format`

```
Here is an example of an array of 10 users consisting of first name, last name, and date of birth in JSON format:

[ { "firstName": "John", "lastName": "Doe", "dateOfBirth": "1990-01-01" }, { "firstName": "Jane", "lastName": "Doe", "dateOfBirth": "1992-03-21" }, { "firstName": "Bob", "lastName": "Smith", "dateOfBirth": "1985-05-15" }, { "firstName": "Samantha", "lastName": "Johnson", "dateOfBirth": "1988-07-30" }, { "firstName": "Charles", "lastName": "Williams", "dateOfBirth": "1995-09-12" }, { "firstName": "Emma", "lastName": "Jones", "dateOfBirth": "1987-11-01" }, { "firstName": "William", "lastName": "Brown", "dateOfBirth": "1994-02-17" }, { "firstName": "Ashley", "lastName": "Davis", "dateOfBirth": "1991-04-23" }, { "firstName": "Michael", "lastName": "Miller", "dateOfBirth": "1986-06-28" }, { "firstName": "Emily", "lastName": "Moore", "dateOfBirth": "1996-08-13" }]

This array contains 10 objects, each representing a user with a first name, last name, and date of birth. The objects are formatted in JSON, which is a standard data interchange format.
```

## Generate how to / step-by-step guides
There might be times where you want simple, detailed how to instructions in order to carry out a testing activity. I'm a big fan of both [Postman](https://www.postman.com/) and [restful booker](https://restful-booker.herokuapp.com/) and wondered whether ChatGPT could help create a step by step guide on how to create a booking within restful booker via Postman.

I asked ChatGPT: `create postman request to create a booking in restful booker`

```
To create a booking in Restful Booker using Postman, you can use the following steps:

1. Open Postman and select the "POST" method.
2. In the "URL" field, enter the following endpoint: https://restful-booker.herokuapp.com/booking
3. In the "Body" section, select the "raw" option and choose "JSON" from the dropdown menu.
4. In the body of the request, enter the following JSON payload, replacing the placeholders with your desired values:

Copy code
{ "firstname": "YOUR_FIRST_NAME", "lastname": "YOUR_LAST_NAME", "totalprice": NUMBER, "depositpaid": BOOLEAN, "bookingdates": { "checkin": "YYYY-MM-DD", "checkout": "YYYY-MM-DD" }, "additionalneeds": "YOUR_ADDITIONAL_NEEDS" }

5. Click the "Send" button to send the request. If the request is successful, you should receive a response with a status code of 201 (Created) and a JSON object containing the details of the newly created booking.

   Note: You may need to first create an account and login to the Restful Booker platform in order to create a booking.
```

## A study buddy
Sometimes you might want to learn more about a specific thing to expand your knowledge. ChatGPT is really useful for this type of thing: `what is equivalence partitioning` 

```
Equivalence partitioning is a software testing technique that involves dividing the input data of a software system into partitions of data that are equivalent in some sense. The idea is to test the system with a representative sample of data from each partition, rather than testing every possible input. The goal is to find and fix defects with the minimum number of test cases.

In practice, equivalence partitioning can be used to divide input data into classes that are expected to behave in the same way. For example, if a system accepts integers as input, you might create an equivalence partition for positive integers, negative integers, and zero, since these are all treated differently by the system. Another equivalence partition might be created for strings that are too long to be accepted by the system, and another for strings of a valid length. By testing the system with a representative sample from each partition, you can ensure that it is working correctly for all classes of input data.
```

I'm pretty sure there's lots of really useful ways ChatGPT can be used to assist testing. Let me know in the comments how you've used it.