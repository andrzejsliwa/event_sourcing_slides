
## ES FAQ
  - [Achieving consistency in CQRS with linear event store - 2015/09 - discussion on Reddit](https://m.reddit.com/r/programming/comments/3l0hp1/achieving_consistency_in_cqrs_with_linear_event/?utm_source=mweb_redirect&compact=true)
  - [Messaging Flavours - kinds of Events](http://verraes.net/2015/01/messaging-flavours/)
  - [Domain Events - 2014/11](http://verraes.net/2014/11/domain-events/)


  - [CQRS with Event Sourcing – Neos - From the Labs - 2016/08](https://www.youtube.com/watch?v=JNt4Wlu16e4)


  - [What is a Domain Event? - 2010/04](http://codebetter.com/gregyoung/2010/04/11/what-is-a-domain-event/)


  - [Event Sourcing - Versioning](https://abdullin.com/post/event-sourcing-versioning/)


Q:
hey guys, question.. is it acceptable for a projection to be reading data from other read models?
or should a projection only rely on the events themselves for updating its state?

A:
There is also a risk that the supporting projection might not be populated with information you require yet depending on how you populate them.
And in turn because of this. If you do replay them you could end up with different results


It is OK to do so… you may face problems when replaying events for that projection, though, as you'd have to re-create the other projections you depend upon as well… Another approach is for your projection to create its own "support only" read models… (perhaps this is what you meant on your second statement?)



Q:
Can someone elaborate on: "The single biggest bad thing that Young has seen during the last ten years is the common anti-pattern of building a whole system based on Event sourcing. That is a really big failure, effectively creating an event sourced monolith."
If we have a well-factored service-based architecture with services integrating over a message bus via domain events, is that an “event sourced monolith”? If so, why?

A:

There's a difference between event sourcing and 'integrating over a message bus' - event sourcing is building your current state from previous events, integrating over a message bus is messaging
I guess what the quote is getting at would be a system where every single service is using event sourcing, which is probably unnecessarily

I.e. Not a 'top level' architectural style

So you could have one service that benefits from event sourcing, but others that are simple CRUD where event sourcing would be over engineering

But they might still integrate using messaging...



Q:


You can have 2 event streams
One is the master which has all granular events and then another stream that's a projection of the other and has the less granular ones. It's just a projection, but can be used to me easily think about state for some business concept.


Q: How do you implement competing consumers?

If you look at the competing consumers implementation in event store
(to be used as a queue) there is a strategy specifically for this
which will keep consumers stable based on a hash EG messages for Foo-1
will always (if possible) be pushed to consumer 1. Foo-57 will always
be pushed to consumer-6. This prevents the issue you discuss and
should work easily at 4-5 orders of magnitude greater than your
load.https://github.com/EventStore/EventStore/blob/release-v4.0.0/src/EventStore.Core/Services/PersistentSubscription/ConsumerStrategy/PinnedPersistentSubscriptionConsumerStrategy.cs#L8

