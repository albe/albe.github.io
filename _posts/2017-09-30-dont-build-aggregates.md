---
layout: post
title:  "Don't Build Aggregates"
categories: ddd
draft: true
---
# Don't Build Aggregates

The Domain Driven Design Community is obsessed about terminology, being precise with language, and yet we fail to name the most fundamental building blocks in a non-misleading way.
This is probably a very hot take and a bit of an overstatement, but bear with me. I'll try to explain.

## Recap: What's an Aggregate (in DDD)

The term "Aggregate" in Domain Driven Design was most likely coined by Eric Evans in his Blue Book, back in 2003.
There, an Aggregate is defined like this:

> An AGGREGATE is a cluster of associated objects that we treat as a unit for the purpose of data changes. Each AGGREGATE has a root and a boundary. The boundary defines what is inside the AGGREGATE. The root is a single, specific ENTITY contained in the AGGREGATE.

## What does the dictionary say?

http://www.dictionary.com/browse/aggregate

> noun
>
> a sum, mass, or assemblage of particulars; a total or gross amount:
> the aggregate of all past experience.

So within the definition from the blue book, the term "Aggregate" somehow makes sense, in so far that it can be considered an "assemblage of particulars".
It's neither a "sum" or a "total or gross amount" of anything though. IMO there would have been less ambiguous names, especially since [`Aggregation`](https://en.wikipedia.org/wiki/Class_diagram#Aggregation) is already a term long used in class diagrams, where it's definition is kind of diametral to the one used in DDD.

## Current state of the definition

In his talk ["What I've learned about DDD since the book"](https://qconlondon.com/london-2009/qconlondon.com/london-2009/presentation/What+I've+learned+about+DDD+since+the+book.html) Evans somehow amended the definition
and stated that too much focus was put on how Aggregates are structured and accessed, while their main concern is about being a `Consistency Boundary` and a conceptual whole.

This is the most widely used definition nowadays by the major DDD sages, though Martin Fowler still focuses the [definition](https://martinfowler.com/bliki/DDD_Aggregate.html) on the structural aspect.

That's the point where the terminology got disconnected from the intended usage. And this usage is emphasized even more when building an event-sourced system, because especially there you shouldn't build a structural model at all, but a behavorial model that reflects your business rules and transactions.
A very good blog post that shows that shift is https://codeopinion.com/clean-up-your-domain-model-with-event-sourcing/
The event-sourced model only contains properties that are required to enforce its business rules.

Yet, we still build `Aggregates` with `Aggregate Root` structural Entity models, possibly capsulating temporal business processes that are not modelled well through a hierarchy of entities.
And then, there are the practitioners that understand the concept and build really process and rule based models, but yet they call them "Aggregates", when they neither contain collections of other objects, nor do they "aggregate" anything. The next wave of developers trying to understand the concept will then try to read up what an "Aggregate" is and come back to the structural definitions and examples from the past.

In the first case we use a wrong model and in the latter case a wrong and misleading terminology.

## It is time to find a better term

I already brought this up quite some time ago (Dec. 2016) with Mathias Verraes on [Twitter](https://twitter.com/ih8nickfinding/status/807275519213522944) and back then the quick consens was that `TransactionalConsistencyBoundary` would be a better term. It at least is precise on the intended usage, but TBQH it's also verbose and very technical.
