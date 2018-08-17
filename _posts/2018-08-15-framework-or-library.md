---
layout: post
title: "Framework or Library!"
date: 2018-08-15 11:25:06 -0500
comments: true
published: false
---

Nowadays everyone is building _Frameworks_. Building a _Software Product_ is so passe!

So here's a brief rundown of some confusing terms:

- A `Software Framework` is something that is complete in itself for default behavior. But to customize it's 
behaivor, it provides extension points where you, as a developer will need to provide your 
own implementation.

- A `Software Platform` is something that provides some hooks for a complete business process. In a 
way, it is  similar to a `Framework` but for business need.

- A `Library` is a set of code that is _invoked_ by your code on demand. Note that there is a 
one-way coupling here your code is dependent on the library but the library is not dependent on your code. 
Also, this coupling is at _build time_.

- An `API`, much like a library, offers the one-way coupling, but it _can also be at runtime_, using
 RESTful verbs over Http. 


Having got that out of the way, let's look at some fantastic feature in `Spring Boot` 
from the `Spring Framework`
that allows you to extend your own applicaton, using the _same_ extension points that _it_
uses when it has to add a


Oftentimes when we are writing an application, we have to make our apps 


Everyone loves frameworks!
None more than software startups!

In the past 10 years I've been involved with (almost) as many startups in the business of building software to make their 
customers' life better. But not one of them deigned to apply the epithet of _software product_ to their efforts!
It's got to be a _Framework_... or better still a _Platform_!

It's alomst as if a _software product_ is for losers! We want a _platform_ on which our happy 
customers will conduct not only their business, but also _their_ customer's business!

This grandoise vision has unfortunately percolated into corporations also where I
find developers who are involved in building some core libraries that other developers will use,
will happily label their project as a Framework when it is nothing but!

So what's the big deal you may ask.. it's just a name, right?
Wrong!
Names are very important and in this day and age where there is so much information to consume, 
we often rely on words in absence of a TL;DR version!

So let's spend some time talking about a `Framework`, a `Platform`, a `Library` and an `API`.

- A Software Framework is something that is complete in itself for default behavior. But to customize it's 
behaivor, it provides extension points where you, as a developer will need to provide your 
own implementation.

- A Software Platform is something that provides some hooks for a complete business process. In a 
way, it is  similar to a `Framework` but for business need.

- A Library is a set of code that is _invoked_ by your code on demand. Note the one-way coupling where
your code is dependent on the library but the library is not dependent on your code. 
Also, this coubling is at _build time_.

- An `API`, much like a library, offers the one-way coupling, but it _can also be at runtime_, using
 RESTful verbs over Http. 




