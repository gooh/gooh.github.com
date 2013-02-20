---
layout: post
title: Modeling the Real World
---

A few days ago, I was asked by [@__edorian][1] whether I'd agree to the statement that developers model the real world. I considered the question briefly and then [replied][2]

> We as Software Developers don't model the real world, we abstract domain concepts into deterministic programs

In this blog post I'll expand on that statement by example.

## The Scenario

Let's say you are tasked to build a Online Car Reservation System (it's always cars in OO tutorials) for a local Car Rental Service. You meet with the client for the first time, she explains her vision to you and after a few days, she hands you the requirements for a first UseCase:

#### UseCase UC1: Reserve Car

**Primary Actor:** Website Visitor
**Stakeholders and Interests:** yaddayaddayadda
**Preconditions:** none

**Success Guarantee (Postconditions):**

- Reservation is saved.
- Rental Cost is correctly calculated.
- Car is reserved at Rental Station
- Reservation Voucher is sent to Website Visitor via eMail

**Main Success Scenario (Basic Flow):**

- Website Visitor arrives at Website
- Website Visitor enters Rental Date and Website Visitor's eMail
- System records selected Rental Date and Website Visitor's eMail
- System determines available cars for Rental Date
- Website Visitor selects Car to reserve
- System records selected Car
- System calculates and presents Rental Cost to Website Visitor
- System secretly sells eMail address to Affiliate Marketer
- Website Visitor confirms Car Reservation
- System reserves Car at Rental Station
- System confirms Car Reservation to Website Visitor
- System sends Reservation Voucher to Website Visitor's eMail

**Extensions (Alternate Flow):** more yaddayaddayadda

Doesn't sound too difficult. On to modeling.

## Don't model the real world

Now, let's imagine you start to model the real world from this UseCase. What do you need? Obviously, the Car. What makes up a Car in the real world? Right, it got a motor, and tires and doors and a trunk and windows and windshield wipers and a fuel tank and an exhaust pipe and a handbrake and seats (dont forget the seats) and an AC and rear view mirrors and &hellip; are we there yet? No, because a Car has a couple thousand parts. And the vast majority of them are meaningless for your client's Reservation System.

What you really want to model is a Car as it makes sense in the Business Domain of our client's Car Rental Service **and** the purpose of the application at this stage.

## Abstract Domain Concepts

So instead of wasting your time creating unneeded complexity, you just look at the UseCase. But since you are not a Rental Agent, you decide to call up the client again to get some reaffirmation about your understanding of how this is supposed to work:

**You:** Hi, can we talk about the UseCase once more? I'd like to make sure I understand what we are talking about before I start coding.

**Client:** Of course. Let me just summarize it in my own words. Our *Clients* can make *Reservations* for specific *Cars* at a certain *Date*. And they should get a *Voucher* for that, which they can carry to our local rental station. And that's where we make the actual *Rental*.

**You:** Ok, about the Car, what's important about it? Is there any particular criteria the Client can pick from when choosing the car?

**Client**: Not really. We only have a dozen cars. Usually we just tell the client which *brand* and *model* that is and how much it will *cost* to rent it. In the summer, the clients often ask whether the car has an air condition, so I guess that is important to note online, too.

**You**: That's pretty simple. I thought there might be more about the Cars.

**Client**: We do keep track of a lot more data about our cars, but for the UseCase it's not important. Let's keep it at the simple level for now.

**You**: Got it. One last thing. Umm, do you really want to secretely sell the eMail adress of the client to an Affiliate Marketer?

**Client**: Haha, no. I was just checking whether you were reading the UseCase.

**You**: Thanks, I think I know all I need to know right now. I'll send you a diagram in a couple minutes, visualizing what we just talked about.

![UML Model for Car Reservation UseCase - powered by yuml.de](http://yuml.me/diagram/scruffy/dir:lr/class/%5BReservation|rentalDate;totalCost%5Dreserves-%5BCar|brand;model;id;price;hasAC%5D,%20%5BReservation%5DconfirmedIn-%5BVoucher%5D,%20%5BReservation%5DmadeFor-%5BClient|email%5D)

## Into Deterministic Programs

Now that you know how to think in the mental model of a Rental Agent, it's time to add your own expert knowledge. The UML above is [good for communicating with your client][4], but it's not a runnable program. Don't confuse it with class diagrams. It's just the conceptual basis.

So the next step is translating your newfound knowledge into something a computer can execute. In this phase, you will design and ultimately code the components you need in the various layers in what the UseCase only calls "the System".

For your client, these details are largely uninteresting. Whether you use a Framework or a particular Design pattern doesn't matter to him. She trusts you to deliver a professional result.

She also likely won't be interested in Class diagrams or similar UML artifacts. Whether you use those is up to you. What counts is that you concentrate on modeling your client's view of their problem domain in a way that allows you and him to communicate and you to build a software system around it.

And that's what my initial statement means.

[1]: https://twitter.com/__edorian "Edorian's Twitter Account"
[2]: https://twitter.com/#!/__edorian/status/165796820608491521 "Quoted Tweet"
[4]: http://domaindrivendesign.org/node/132 "supports Ubiquitous Language"