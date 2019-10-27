## Chapter 2 The unified log

### Anatomy of unified log

* A unified log is an append-only, ordered, distributed log that allows a company to centralize its continuous event streams.

#### Unified

* Single deployment of technology, with multiple applications sending events to it and reading events from it.
* Kafka is designed to allow a single cluster to serve as the central data backbone for a large organization.
* Use separate log streams depending on business domains from which you're working.

#### Append only

* Append-only means that new events are appended to the front of the unified log, but existing events are never updated in place after they're appended.
* Events are automatically deleted from the unified log when they age beyond a configured time window.

#### Distributed

* Scalability in its implementation is spread across a cluster of machines; provides scalability log streams storage and availability is provided by the cluster of machines.
* Durability, data loss risk is minimized by replicating logs across the cluster.

#### Ordered

* Ordered, means that the unified log gives each event in a shard a sequential ID number that uniquely identifies each message within a shard.

### Events construction

* subject->verb->object
* Eg. 'shopper views product at time', 'shopper adds item to a cart at time', 'shopper places order at time'.
