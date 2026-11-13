# Operating Systems: Concurrent Request Processing

A Java concurrency exercise that models requesters, assigners, and workers.
Requests pass through bounded queues and semaphore-protected dispatchers before
their results are returned to the originating requester.

## How the simulation works

- **Requesters** generate numbered requests and wait for their responses.
- **Assigners** select workers using assignment counters.
- **Workers** process values and simulate interruptions and restarts.
- **Queues and dispatchers** coordinate access with `java.util.concurrent.Semaphore`.

All classes are included in
[src/it/unifi/Main.java](src/it/unifi/Main.java).
The default configuration starts three requesters, twelve assigners, and six
workers, with a bounded queue of one hundred requests.

## Build and run

A JDK is required. The source uses Java 7-or-later language features; it is a
historical exercise and includes deprecated thread-management APIs.

From the repository root:

```sh
javac -d out src/it/unifi/Main.java
java -cp out it.unifi.Main
```

The driver runs for approximately twenty seconds before initiating shutdown and
printing worker restart and assignment statistics. Output order and results
vary because the simulation uses concurrent threads and randomness.

## Exploring the code

Change `N`, `M`, `K`, and `R` in `Main.main()` to explore different requester,
worker, assigner, and queue configurations. The same file contains the
`Requester`, `Assigner`, `Worker`, `Queue`, `ReqDispatcher`, `Request`, and
`Counter` classes.

This is a teaching simulation, not a production task scheduler. In particular,
it uses the deprecated `Thread.stop()` API; review thread lifecycle and shutdown
behavior before adapting it to a modern JDK or a real service.

## Project provenance

This repository is a fork of
[edoardore/ProgettoSistemiOperativi](https://github.com/edoardore/ProgettoSistemiOperativi).
The original implementation and history are preserved.
