---
tit: What is Apache Kafka?
tags:
  - system-design
  - messaging
  - pub-sub
description: Introduction to pub/sub and Apache Kafka
---
Kafka's core concepts can be listed as:
- Event streams
- Topics
- Brokers
- Producers
- Consumers
- Dispersing streams into unified realtime pipelines
- Realtime data bus, allowing different microservices to talk to each other
- Monitoring and observability -> ELK Stack
- Resource intensive and quite complicated at first glance

think about an e-commerce. when a customer places an order, a chain of events must happen to correctly process that placed order, like updating stock in database, sending purchase confirmation notification to customer, updating analytics data boards and so forth and so on.
in a microservice architecture, that would happen through microservices calling each other. separate microservices sending data throughout them and taking all those necessary actions aforementioned. that's a tightly coupled architecture.
that's called **Tight Coupling**. each service directly calls the other, if one is down, everyone else gets affected and the entire order process is disrupted. one slow service and everything slows down. 10 minutes of outage means hours of orders backlog. the list goes on.
what if we could remove that tight coupling? what if something can sit in the middle of an order being placed and a notification being sent to our customers?

Seller -> Post Office -> Buyer
a seller never delivers a package to the buyer themselves. they send it to a post office, so they take care of delivering the package to whoever bought it. Kafka is the post office.
it takes care of receiving a package and making it available to whoever needs it, aka, the buyers. now, whoever left that package in the post office does not need to be concerned about it once they drop it, they can go back to their own duties and let the post office handle it.

"leaving a package" is called publishing an event. an event is the 