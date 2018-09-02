---
layout: post
title: "Integrate Stripe easily into your Spring Boot apps"
date: 2018-09-01 11:25:06 -0500
comments: true
published: true
---


[Stripe](https://stripe.com) is the popular Payment Gateway that allows websites' owners to make money by accepting payments online.
The [Stripe API](https://stripe.com/docs/api/java#events) deals with the complicated stuff like _Credit Card data, security and PII_ and offers an API that will allow you,
the website owner/developer to deal with the easy stuff.

This _easy stuff_ falls in four categories:

1. Stuff you do one time during Stripe account setup:
   - Setting up the Project (aka `Product`). Typically this is one  per website.
   - Setting up Payment `Plans` - How often and how much will your customers pay you.
   - Setting up `Coupons` - these are discounts/promotions that are set up per plan.

2. Stuff that needs to happen with every user sign-up, or purchase:
   - Creating a `Customer` - happens when a user registers on your website.
   - Creating a `Subscription` - ties a Customer to a Plan.
   - Creating a `Transaction` - When a charge is made.

3. Stuff that is done behind the scenes at a pre-configured cadence by Stripe:
   - Prepare `Invoices`
   - Prepare scheduled reports

4. Events
   - Provide notifications via callbacks when pre-defined events like `charge.succeeded`, `customer.created` etc occur.


When integrating this rich Stripe API with your application, the first question that has to be answered is:

_What data should be maintained in the data model of your app, and what data should be maintained in Stripe (in the cloud)?_.

The answer to that of course is based on performance, audit and storage constraints. But if addressed purely on the basis of data redundancy,
the single link that ties the two models together is the Stripe `customerId`.

<p align="center">
  <img src="{{site.baseurl}}/images/stripe.png" width="600" height="400"/>
</p>

As we can see above, Stripe's `customerId` is mapped to the app's `userId` (which is the the `Id` of the `User` object in the Widget Spring Boot App).
Everything else can be retrieved and manipulated via the [StripeService](https://github.com/pankajtandon/stripe-starter/tree/master/stripe-service) by supplying it the `customerId`.
Using the `customerId`, which would be typically mapped, one-to-one with the UserId, the [StripeService](https://github.com/pankajtandon/stripe-starter/tree/master/stripe-service)
can be used to manipulate and access all other entities that are maintained in on `Stripe`.

In it's current state (`version 1.0.2`), StripeService offers limited functionality. For those features not exposed via this service, the base
'Stripe API` may be accessed. But most commonly used scenarios are described in the readme docs of the service [here](https://github.com/pankajtandon/stripe-starter#common-use-cases).

Based on the categories of features offered by Stripe (described above), `StripeService` offers features in category 2 for now.
The other categories represent one-time actions that can be carried out via the [Stripe Dashboard](https://dashboard.stripe.com/developers).

If your app is built using [Spring Boot](http://spring.io/projects/spring-boot), incorporating `StripeService`
is even easier via the accompanying [Starter project](https://github.com/pankajtandon/stripe-starter/tree/master/stripe-spring-boot-starter).