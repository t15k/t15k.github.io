---
layout: post
title:  "Polymorphism and schema technologies"
---

I read the [Confluent blog post] on Single vs multiple types on Kafka topics.
Excellent considerations by Martin Kleppmann, and I definitely agree with
sticking to to having only one type per topic. However I think Kleppmann leaves
out one design, that I've seen work very well, when balancing between
introducing a new topic or putting more messages type on an existing topic.

Some mixed types
=================
Let's take a look at some data where that we might want handled in a single
place, but which are still different types, from data modelling perspective.
Here are two
snippets, one being a email like kind of message, the other being an SMS
or Twit kind of message.

```json
{"id": 123, "subj": "Greet", "body": "Hello", "to": "some@one.se"}
{"id": 124, "text": "Hello there", "to": "some@one.se"}
```

On a stream of data containing both, a processor must then either check for the
existence of properties that marks the message as appropriate for processing.
This is easily done

```python
if msg.has_key("body"):
  handle_email_message(msg)
elif msg.has_key("text"):
  handle_simple_message(msg)
else:
  handle_unknown_message(msg)
```

However, this can quickly become hard to mannage. Let's say a new message type
is logged that also has _msg_ property. We would incorrecly handle that as an
email in the snippet above.

Make them polymophic
======================
The trick is to uniform the messages and make them polymorphic. So rather than
the JSON from above, this is preferred.

```json
{"id": 123, "subj": "Greet", "text": "Hello", "to": "some@one.se"}
{"id": 124, "text": "Hello there", "to": "some@one.se"}
```
Now rather than having function dedicated message types, we can re-organise the
handling code to this.

```python
handle_text(msg)
handle_to(msg)
```
We can now handle multiple types on the same topic, thanks to making them polymorphic.








[Confluent blog post]: http://bit.ly/ct-type-kafka-topic
