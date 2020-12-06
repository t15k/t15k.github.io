---
layout: post
title: Stored procedures
---

This post is inspired by this [tweet on stored procedures]. The many opinions
on wether their usage is a good or a bad idea, made me think try an put together
structured walk-through of things to consider.

Tiers
===

Let's pretend we have a service that fetches customer orders and displays them
to a user. It will involve a client (C) which which initiates requests and
handles display, some presentation logic (P) that will present data to the user
in a format  and shape (i.e. HTML) that is suitable for the client. Finally
we have a system for persisting D.

    C <-> P <-> D

Let's further say that D is a system, where we can also deploy logic that
will operate on the data and that an appropriate protocol is shared
between client and systen, so they can comminicate directly.
That leaves us a few options.

Deploying logic in the server
---
The first one is that we simply put our presentation logic on the server. This
gives that will work. This will typically gives us a simple deployment mode,
as we already require the data system, and it gives us quick access to the
data, as they are in same system.

However, there is a 

Keeping logic in seperate process
---

There are occasions where having a separate process is required. If the client
and the data system, cannot communicate on the same protocol, we need a bridge
in between to translate from one protocol to the other.

- Access logic
- Rendering logic.
- Protocols
- 




[tweet on stored procedures]: https://twitter.com/springrod/status/1152757171475476480?s=20