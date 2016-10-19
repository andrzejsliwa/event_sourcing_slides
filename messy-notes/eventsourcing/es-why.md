- http://udidahan.com/2010/11/15/the-known-unknowns-of-soa/

But the question remains, if a producer/consumer relationship is OK for SOA-type services, why doesn’t that hold for web services? And the answer is… it depends on the type of producer/consumer relationship. The typical relationship is one of synchronous calls from consumer to producer, this is not OK for SOA-type services either.


You see, this synchronous producer/consumer implies a model where services are not able to fulfill their objectives without calling other services. In order for us to achieve the IT/Business alignment promised by SOA, we need services which are autonomous, ie. able to fulfill their objectives without that kind of external help.


Instead, we need to look for a more loosely coupled producer/consumer relationship – like publish/subscribe, where the producer emits events, and the consumer subscribes and handles those events.

The reason that this kind of relationship doesn’t hurt autonomy is that it disconnects services on the __dimension of time__.

In order for a service to be able to make a decision autonomously without synchronously calling any other service, using only information provided by events it received in the past, it must be strongly aligned with the business.


