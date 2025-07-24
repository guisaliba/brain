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
a seller never delivers a package to the buyer themselves. they send it to a post office, so they take care of delivering the package to whoever bought it. **Kafka is the post office**.
it takes care of receiving a package and making it available to whoever needs it, aka, the buyers. now, whoever left that package in the post office does not need to be concerned about it once they drop it there, they can go back to their own duties and let the post office handle it.

"leaving a package" is called publishing an event. an **event** records the **fact that something happened** in our e-commerce business, they are also called **record** or **message**. they are simple key-value structures, that also contains a timestamp and some optional metadata (like information about the order, the customer who placed it, etc).
when you read or write data to Kafka, you do this in the form of **events**.

so now the order microservice does not need to wait for a response, they can just publish an event to Kafka, and leave it to be. if a service publishes (write) an event into Kafka, they are called **producers**. this is done through the Producer API, to produce and send events.

but where do events go? since many services can be producers and send events to Kafka, how Kafka organizes them and store each event? that's where **topics** come in.
a **topic** is a section of the post office, a department, that group and store the same type of packages. for example, the order service will publish orders to the order topic. a topic is defined just like a schema in a database, the developer decides what and how they look like.

what next? packages are safely stored in their own departments, but how does the department handles these packages to all those buyers waiting to receive them?
**consumers** are the buyers, that will **listen to a topic** (a department) of the post office, waiting for any package that arrives there in that topic. 
a consumer is just another service, like the producers, but they don't write data to Kafka, they read it instead and take their own actions whenever something is read.

Kafka is not a replacement of a database.

a chain reaction of **events** is the result of multiple events happening based on the publishing of one event as seen before. for example, a service publishing an order event to the order topic may cause a service listening to that topic publish an event to an inventory topic.
then, someone can be listening to that inventory topic and produce an alert for products below the stock threshold, publishing another event to another re-stock topic. everything is a domino.

real time processing in Kafka are also called **streams**.