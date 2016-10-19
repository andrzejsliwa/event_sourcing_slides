-------

- Greg has often said that the projects where you want to do Domain Driven Design are those projects where the business has a competitive advantage.

-------
- The future is the function of the past... (A. P. Robertson), australian math teacher..
-------

https://groups.google.com/forum/#!topic/dddcqrs/iHzPzaNMo-w
- In *most* real-life mature business processes, the businesses have come to accept that it's better to detect the problem after the fact (product is back-ordered, bank balance is overdrawn, etc) and take compensating actions.


In my experience, the trick is to get the people driving the requirements to move past "Users can't overdraw their bank account", to admit -- "well, right now, if they overdraw their accounts..." and move towards a requirement that looks more like: "Users should be prevented from overdrawing their bank account if possible, BUT..."




-------
Going to microservices is like going from Newton’s physics to Einstein’s physics. Newton’s time marched forward uniformly with instant knowledge at a distance. Before microservices, distributed computing strove to make many systems look like one with RPC, 2PC etc.. In Einstein’s universe, everything is relative to one’s perspective. Microservices has “now” inside (a service) and the “past” arriving in messages.



-------
- The (local) present is a merge function of multiple concurrent pasts. (Jonas Boner, author of Akka (actor model))

- Information is always from the past
- if we are wrong, we take a compensating action
  - appology oriented programming
- we need to treat time as a first class construct, needs to be explicit
- the past is immutable

- mutable state should be contained
  - use only for local compuation, within safe island
  - those changes should be non-observable to the rest of the world


- functional programming
  - functions are fact machines
    - you put facts in, and facts come out

  - gives you code, that you can trust
  - functional programming done right is referentially transparent
- never delete facts

- database is a cache of a subset of the log, the truth is in the log.

- keeping all the history used to be very-very expensive

- today it just does not make any sense.
- storage is incredibly cheap


- event log gives us a database not just about the present, but database of the past. and this is incredibly powerful. auditing, debugging, for data-mining, etc.

- allows us to shift our focus from data at rest, to data in motion.


- first we need to find the units of consistency
- decompose the system using consistency boundaries
- once done, this consistency boundary can never be violated, can never be partitioned. It needs to be moved as a whole, stored as a whole entity. If we try to break it approae

- microservices has nothing to do with size
  - single responsibility
  - isolation
  - share nothing design
  - needs to own their data
  - extend the consistency boundary not just around behaviour, but also around data
  - should be one unit, that moves and replicates as whole
  - it can't be default done through REST
    - REST can be asynchronous
    - synchronous communication between microservices is an anti-pattern
    - it can sometimes be important, but it is a really bad default

    - you should rely on asynchronous communication


- decoupling in time / space
  - location transparency
  - async communication
  -
