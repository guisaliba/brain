---
id: "866e677a-dc2b-48e0-9a3b-f69873f00d75"
title: "Difference between a Service class and a Helper class"
source: "https://softwareengineering.stackexchange.com/questions/132067/difference-between-a-service-class-and-a-helper-class#:~:text=Infrastructure%20Service%3A%20These%20are%20used,without%20violating%20the%20DRY%20principle."
aliases: ["Difference between a Service class and a Helper class"]
---
A Service class/interface provides a way of a client to interact with some functionality in the application. This is typically public, with some business meaning. For example, a TicketingService interface might allow you to buyTicket, sellTicket and so on.

A helper class tends to be hidden from the client and is used internally to provide some boiler plate work that has no business domain meaning. For example, let's say you wanted to convert a date into a timestamp in order to save it to your particular datastore. You might have a utility class called DateConvertor with a convertDateToTimestamp method that performs this processing.

Services are not simply tightly coupled to DAOs, it's a broader term/usage pattern than persistence

Helper classes do not violate SRP if coded in accordance with that principle. That is, each method should do one thing and one thing well, the class should perform one type of utility help, (e.g. Date conversion) and do that well.