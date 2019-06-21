# Mocks and edges

Mocks are use full for simulating objects, we cannot efficiently
test locally in unit tests.

Objects that are to test are often objects that proxy access
to external systems like Databases or HTTP servers. Using such objects
directly in tests will require such external system to be available.
At best that will slow down our test. At worst that those systems
will maintain state between test, which can influence future tests,
making our tests non-deterministic. Even worse those system may share
state with other concurrently running test, hurting predictability even
further.

This post focuses on how to design for isolation and having
confidence when moving from tests to actual integration.

# Ground rules

1. Mocks belong on the edges og your application,
   if you mock you internal objects,
   something is broken in the fundamental design.
2. 

[Mockito]: https://www.mockiti.org