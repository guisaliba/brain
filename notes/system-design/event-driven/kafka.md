---
tit: Kafka
tags:
  - system-design
  - messaging
  - pub-sub
description: A comprehensive overview of Apache Kafka and pub/sub architecture.
---
think of an e-commerce: when a customer places an order, a chain of events must happen to correctly process that placed order. like updating stock in database, sending purchase confirmation notification to customer, updating analytics data boards and so forth and so on.

in a microservice architecture, that would happen through microservices calling each other.  separate microservices sending data throughout them and taking all those necessary actions aforementioned. that's a tightly coupled architecture.

that's called **Tight Coupling**. each service directly calls the other, if one is down, everyone else gets affected and the entire order process is disrupted. 

one slow service and everything slows down. 10 minutes of outage means hours of orders backlog. the list goes on. what if we could remove that tight coupling? what if something can sit in the middle of an order being placed and a notification being sent to our customers?

**Seller -> Post Office -> Buyer**
a seller never delivers a package to the buyer themselves. they send it to a post office, so they take care of delivering the package to whoever bought it. **Kafka is the post office**.

it takes care of receiving a package and making it available to whoever needs it, aka, the buyers. 

now, whoever left that package in the post office does not need to be concerned about it once they drop it there, they can go back to their own duties and let the post office handle it.

"leaving a package" is called publishing an event. an **event** records the **fact that something happened** in our e-commerce business, they are also called **record** or **message**.

they are simple key-value structures, that also contains a timestamp and some optional metadata (like information about the order, the customer who placed it, etc.).
when you read or write data to Kafka, you do this in the form of **events**.

so now the order microservice does not need to wait for a response, they can just publish an event to Kafka, and leave it to be.

if a service publishes (write) an event into Kafka, they are called **producers**. this is done through the Producer API, to produce and send events.

but where do events go? since many services can be producers and send events to Kafka, how Kafka organizes them and store each event? that's where **topics** come in.

a **topic** is a section of the post office, a department, that group and store the same type of packages. for example, the order service will publish orders to the order topic. 

a topic is defined just like a schema in a database, the developer decides how they look like.

what next? packages are safely stored in their own departments, but how does the department handles these packages to all those buyers waiting to receive them?

**consumers** are the buyers, that will **listen to a topic** (a department) of the post office, waiting for any package that arrives there in that topic. 

a consumer is just another service, like the producers, but they don't write data to Kafka, they read it instead and take their own actions whenever something is read.

a chain reaction of **events** is the result of multiple events happening based on the publishing of one event as seen before. 

for example, a service publishing an order event to the order topic may cause a service listening to that topic publish an event to an inventory topic.

then, someone can be listening to that inventory topic and produce an alert for products below the stock threshold, publishing another event to another re-stock topic. everything is a domino.

real time processing in Kafka are also called **streams**. a stream is a continuous real time flow of records (key-value pairs). 

let's imagine a service that needs to send real time data (such as the location of a person) constantly, updating the user UI with that information (the location).

for such use cases, Kafka uses what is called **Streams API**. it is different from the so far described architecture of producers publishing and consumers processing one event at a time.

streams will process continuous flows of data, providing higher-level functions like transformations and stateful operations like aggregatiosn (counts, averages, sums) and joins.

in code, the Kafka Streams API library leverages the creation of a **stream** to perform stream processing by reading from a topic, processing realtime data and output it to many topics.

and how does that scale? if our e-commerce grew to be large and process a huge amount of realtime data and many event publishing, how would we deal with such an amount?

since we already have sections (departments) in our post office (Kafka), we could just add more workers to each department as needed.

in Kafka that's called **partitions**. if a topic gets overloaded, you smartly decide how to partition your topic, just like a schema design.
do you need more workers to deliver packages to the EU? or the US? it's a design decision.

what about the consumers? if producers can write to multiple partitions and the same time, how does the buyers receive all of these packages at the same time too?
the partitions workers are being super efficient now but how consumers handle all of that?

that's where **consumer groups** comes in. applications that are consumers can be grouped into a consumer group, so replicas of the same application must share the same consumer group id once they are created.

this way, Kafka keeps track of everyone that should receive those events, even if there's 100 instances of the same application waiting for them to arrive.

Kafka distributes the load automatically by assigning partitions to consumers, so when a partition finishes delivering events to a consumer, they can be reassigned to another one.

and last but not least, where is all of this data physically saved? in the Kafka **broker**.
data in topics is saved in Kafka "servers" called brokers. each broker can be thought of a post office branch. 

topic's partitions are distributed across multiple branches (brokers).
if a broker goes down, that partition is also stored in another one, so they don't end up being completely lost or forgotten in the package delivering line.

that's what makes Kafka different from standard message brokers. in services like SQS, when a message is consumed, it is deleted. in Kafka, an event (or a package) is stored as long as you need.

that period is a custom configurable **retention period**. this enables real time data processing, so consumers can read those events anytime they want, even multiple time if they need to.

Kafka focus on event streaming and long term data-retention, while message queueing services focus on delivering a message with reliability and that's it.

watching Netflix is just like Kafka. consumers (viewers) can watch whenever they want, at their own pace and even replay whatever they want.

traditional message brokers are like TV. they just broadcast live (or at a scheduled time) and everyone needs to watch the same thing at the same time. if viewer misses a show, it's gone.

to coordinate all of the scattered post office branches, Kafka has a guy to keep track of everything that happens between those branches (brokers) and coordinate everyone.
that guy is the **Kraft** (or K-Raft), introduced in Kafka 3.0 and later versions.