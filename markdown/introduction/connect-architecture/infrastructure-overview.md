---
title: Infrastructure Overview
stoplight-id: y4jhf67xa1sm0
---
# Infrastructure Overview


 The Shopgate CONNECT backend consists of a microservice
 architecture built with stateless container technology
 and hosted by Amazon Web Services (AWS). Shopgate
 CONNECT is optimized for high availability, scalability,
 and security. The following diagram shows the main
 components of the request flow.


!["Infrastructure Overview"](../../../assets/infrastructure-overview.png)


Incoming requests from the app are load-balanced and
 served by an application proxy which routes them to one
 of the available containers dedicated for this
 particular app. Because you might have custom code
 running inside these app containers, they are located
 outside of the trusted zone (which only consists of
 CONNECT core components) and separated from each other.


 Because all containers are stateless for easy
 scalability, the state of an app is maintained in the
 Cassandra database. The high-performance Cassandra
 database technology enables seamless scalability even
 across regions. The database is highly protected by a
 token-based authorization mechanism. The app proxy
 equips every request with an access token based on the
 current app, user, and session. The access token is
 passed to the database access layer, which then checks
 every single database interaction.


>**Next:**
>
>[Backend Communication](backend-communication.md)
