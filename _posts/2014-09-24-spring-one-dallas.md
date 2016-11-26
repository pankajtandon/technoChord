---
layout: post
title: "Spring One - Dallas"
date: 2014-09-24 16:25:06 -0500
comments: true
---

I’ve just returned from a 3 day trip to [Spring One @ Dallas](http://springone2gx.com/) where I met and heard from several of the smart people who fuel the Spring Framework.

I could only attend 10% of the [break out sessions](https://2014.event.springone2gx.com/schedule/2014-09-09) because of parallel tracks. But there was a buzz in the 
air and in the [NFJS](http://nofluffjuststuff.com/home/main) sessions and if I were to draw a tag cloud of those conversations, 
here is what it would look like:

<p align="center">
  <img src="{{ site.baseurl}}/images/tagCloud.png"/>
</p>

Yeah.. SpringBoot and Spring XD ruled! The keynote was on these two projects too!

But in the end and after attending a couple of sessions, I concluded that Spring Boot is an CoC project that does the following:

Helps you to bootstrap your project by asking the user what he wants to build (webapp, JMS, JPA etc)
Deploys the app in what ever (default) container depending on the type of app (Tomcat, Rabbit, Jetty etc)
To me this seems to be a souped up combination of Maven archetypes and Spring Roo.

But what about Grails, you may ask. Is that not also a CoC framework that does just that: scaffold out your app based on a series of questions?

It does, but the difference is that the Grails user is attempting to build a webapp, which falls under the definition of application development (appdev). Spring Boot, OTOH, results in faster startups and deployments! And while it's true that appdevs do indulge in startups and deployments, I'll be surprised if they do more than a couple of startups and deployment a year! The folks who do startups and deploys all the time are the folks who are developing Proofs of Concepts (PoC), much like the speakers at this conference! No wonder, all speakers were swearing by the virtues of Spring Boot!

And so, instead of serving the appdev community, the good folks at Spring have based the keynote on a product that serves the needs of speakers at the conference! And consultants!

And so I feel that by focussing on Spring Boot, the Spring community has become a self-serving community!

The other big ticket item was **Spring XD**:

I am sure that a lot of work has gone into Spring XD development and I am, by no means trivializing it. It is a great effort, but it is more of a reference implementation of an app well done! I cannot imagine that any corporation will be willing to build out an application that uses all the technologies that Spring XD brings together, and not look under the covers! And if you *did* take the trouble to look under the covers, then you may as well configure the absolutely excellent projects which hold up Spring XD, like Spring Integration, Spring Batch, Spring Data, Spring AMQP, Spring Security etc. And pick and choose what parts of Spring XD it would like to incorporate in your own application.

Moving on, the next big thing was **MicroServices**. Now, like a lot of old concepts which Spring has brought to the masses (like Coding to Interfaces, Inversion of Control, Aspects), the time for MicroServices is here.

With the advent of Reactive Programming paradigms, it makes total sense to slice the pie vertically. Where traditionally, we were layering horizontally around cross cutting concerns like presentation logic, data access logic, persistence etc, now we need to build micro services around bounded contexts. The way these microservices communicate and authenticate with each other is what a lot of talks covered.

And the last topic that was given a lot of air-time was **Groovy**.

Spring has been pushing Groovy for about a decade now and it serves well to provide support (via DSLs) in many areas; the two main ones being build systems (gradle) and Web development (Grails). But now with the advent of Java 8 and Lambda expression support, the value proposition of Groovy seems to have lost a a little bit of steam.

But... the main advantage, IMO in Groovy and other loosely typed languages (Scala, Ruby, Javascript etc) is their adhoc nature and their ability to quickly build DSLs. Java with all its fanfare and ceremony is for the old guys like me!

But…. Like I said, these are first impressions based on only the 10% I attended and the buzz I caught. I haven’t watched the videos yet but when I do, I may change my mind.