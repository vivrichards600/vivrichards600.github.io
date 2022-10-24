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
In this point, I want to talk about how we
as teams can start the test sooner when
it comes to APIs.

Typically you may assume that you need
an API in place to be able to start to
make requests and receive responses and
to test the various states that an API
could be in. Well today we're going to be looking at postman and we're going to be
seeing how we can start to use mocking to
our advantage so let's head over to
postman and take a closer look
so within postman we can either click on
new
and click on mock server or we can just
go unlock service on the left hand side
and click on create mock server
so we're going to just create a simple
get request first and we're going to
call this
um
[Music]
just ping
so when we call the url ping for a mock
endpoint we want to return 200
and we'll just return
ok
in the body next we'll click on next
and we'll call this mock server
test flicks
and we will say save the mock server url
as a new environment variable and we'll
click on create mock server
so now if we go to collections we can
see we've got a new collection called
test flex
with a new
request
called
ping
and this is showing red unresolved
variable
so at the top what we can do is we can
click on environments and click on test
flex
and then you'll see the url is becoming
orange so on the left as well we can
also click on environments and you can
see it created when we create the mock
server test flex
with the url
and the value and also you can see we've
now got our mock server which is test
flex
and mock server with which is test flick
sorry
so if we go back now to the collections
and we click
on send for this request
we can see that we got back our 200 okay
but what about if we now want to call
this endpoint again but to
sort of mark a different response
so what we can do now is we can click
here and we can click on add example
and now what we can do is we can say
let's get a new response and this will
return back a
uh 404 not found
so let's save that and we'll say uh the
response is error
for example
now let's go to the ping endpoint again
and click on send
so now we're just getting 404 error
coming back because that was the first
example within this collection
let's rename this to
404 and let's rename ping to
402 202 sorry at 200 even
for okay i'll send the request again
so it's still returning 404 so how can
we now
within our examples for this endpoint
for the mark endpoint how can we get it
to return back the status code that we
want
so within the get request if we go to
headers
postman has a concept of x mark response
code
or response name
so you can either say i want to
pull back the mock response by the
states code that the example has or by
the name so we've called this 404.200.
so now i'm going to say
return back
the response code
200 or the example 200 and there you see
we've got the 200 back
and if we were to change
this to 404
then we get the 404 back error
so that's great if we want to start to
send requests and get responses back for
the same endpoint but what about if we
want to start to use parameters
so for this let's create a new endpoint
not a new request sorry
and we're going to call this um
speaker
so here we need to copy the url again
and what we're going to do is we're
going to say
we're going to get speaker
by
id
and it can be get request
and we're going to add an example
so here this is going to return back to
200 okay
and we're going to return
maybe the id that was passed to this
request
and we're going to return
maybe the first name
and i'll just put my name for now
and last name
and we'll just
save that example
so now if we click on
get request and we click on send
what happens
so you see that it returned 200 and it
returned my first and last name
but we've got this weird thing here
where it doesn't know what to do with
the id
so now what we can do is we're saying
that this is a parameter called id
and we're saying within the example
we're going to pass an id and then just
use it here
so if we go back and we click on send
now you see the id is being passed
through so every time that we make the
request
and we change that id
the id is just passed through which is
quite nice
so we could take this a little bit
further so postman has a concept of
dynamic variables so what we could do is
we could say
uh
name maybe so we could say random first
name
so let's copy that
and let's put that in our example
and let's go
um
random last name as well just to try and
make this quite nice
and let's see what happens
sorry this bracket's really important
just add this in
so let's make that request and see what
happens
cool so now we have an end point
where every time we send a request off
it's dynamic which is quite nice to be
able to test the responses coming back
but what about so
i mentioned that i could pass through
different ids and the dates dynamic
which is great
but what about when we get to the
speaker whose id is maybe five
we want to return back a 404 just for
that id
so here you'll see that we've got a
request which is to the endpoint
for speaker and then just dynamic id
if we were to just copy this
and we put this to
five and then if we keep that as id
well actually we could just put
speaker not found maybe
and we'll return a 404 not found okay
so what we've got again we've got url
where we're passing the id
but when we pass number five we're
expecting four or four not found so
let's make that request to number four
again make sure we haven't broken
anything
number three maybe number six
and then number five
so there you have it what we can start
to do we can mock requests and responses
by calling the exact same
endpoint
but we can tell what and what states
code to return back or we can mark
responses where we can say for
particular parameters we want to return
back certain responses
so that was just a brief look at postman
and the power of mocking and i really
hope it's given you a few ideas of how
you can start the test api sooner thanks
again for joining the session enjoy the
rest of your day