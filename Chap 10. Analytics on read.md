## Chapter 10 Analytics on read

### Analytics on read

#### Process

* Write all of our events to some kind of event store.
* Read the events from our event store to perform an analysis.

#### Parts

* Storage target to which the events will be written.
* Schema, encoding, or format from which the events will be written to the storage target with.
* Query engine to allow us to analyze the events in the storage target.

### Analytics on write

#### Requirements

* Very low latency, real time systems will be built off the analytics produced.
* Supports thousands of simultaneous users.
* Highly available, business decisions will be made from the interpretation of the analytics produced.

#### Process

* Read our events from our event stream.
* Analyze our events by using a stream processing framework.
* Write the summarised output of our analysis to a storage target.
* Serve the summarised output into real time dashboards or reports.


