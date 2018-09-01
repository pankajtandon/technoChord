---
layout: post
title: "Integrate Stripe easily into your Spring Boot apps"
date: 2018-09-01 11:25:06 -0500
comments: true
published: true
---

Integrate Stripe easily into your Spring Boot apps

Stripe is the popular Payment Gateway that allows websites' customers to pay you, the website owner. It deals with the complicated
stuff like Credit Card data, security and PII and offers an API that will allow you to deal with the easy stuff.

This `easy stuff` falls in four categories:

1. Stuff you do one time during Stripe account setup:
   - Setting up the Project (aka Product). Typically this is one  per website.
   - Setting up Payment Plans - How often and how much will your customers pay you
   - Setting up coupons - these are discounts/promotions that are set up per plan

2. Stuff that needs to happen with every user sign-up, or purchase:
   - Creating a customer - happens when a user registers
   - Creating a subscription - ties a user to a Plan
   - Creating a transaction - When a charge is made

3. Stuff that is done behind the scenes at a pre-configured cadence by Stripe:
   - Prepare Invoices
   - Prepare scheduled reports

4. Events
   - Provide notifications via callbacks when pre-defined events like charge.succeeded, customer.created etc occur.


When integrating this rich Stripe API with your application, the first question that has to be answered is:
__What data should be maintained in the data model of your app, and what data should be maintained in Stripe (in the cloud)__.

The answer to that of course is based on performance, audit and storage constraints. But if addressed purely on the basis of data redundancy,
the single link that ties the two models together is the `customerId`.

<p align="center">
  <img src="{{site.baseurl}}/images/stripe.png" width="600" height="450"/>
</p>

As we can see above, the `customerId` is mapped to the `userId` which is the the `Id` of the `User` object in the Widget Spring Boot App.
Everything else can be retrieved via the Stripe API by supplying it the `customerId`.

The [StripeService](https://github.com/pankajtandon/stripe-starter), offers functionality in category 2 above. The other categories are one-time actions that
can be carried out via the [Stripe Dashboard](https://dashboard.stripe.com/developers).

To make it still easier to incorporate into your Spring Boot project, you may want to consider the much easier [stripe-spring-boot-starter](https://github.com/pankajtandon/stripe-starter)
 project.