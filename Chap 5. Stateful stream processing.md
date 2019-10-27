## Chapter 5 Stateful stream processing

### Stream processing frameworks

* State management, state allows processing of multiple events which do not lie in the same stream processing window.
* Stream windowing, bounded windowing for the event processing, time based or event count.
* delivery guarantees, frameworks provide guarantees of events processed at least once. Extra to this would be transactional gurantees that each event is processed only once.
* Task distribution, frameworks are designed to run on similar cluster infrastructure as the stream itself. Eg. Kubernetes, Mesos where scaling horizontally is provided through the infrastructure.
* Fault tolerance, fault tolerance typically involves a distributed backup of either the incoming events or the generated state.

### Frameworks

* Apache Storm, fault tolerance is achieved by record acknowledgements with upstream record backups, rather than state snapshots or checkpoints. Nimbus was a purpose built scheduler. Exactly once processing is supported by separate library Storm Trident.
* Apache Samza, stateful stream-processing, is tightly integrated with Apache kafka.
* Apache Spark streaming, is a microbatch processing framework, batches are then feed into the existing spark processing framework.
* Apache Kafka streams, Kafka streams was designed from the start as a library to be embedded in your application code. Kafka streams uses Kafka for all aspects of its state management, fault tolerance, and delivery guarantees.
* Apache Flink, designed from the beginning to be a streaming framework. Supports exactly once event processing, is closely aligned with the Apache Beam project.

### Yarn

* Yet Another Resource Negotiator.
* ResourceManager, central 'brain' that tracks servers in the Hadoop cluster and jobs running on those servers, and allocates compute resources to these jobs.
* NodeManager, Runs on every server in the Hadoop cluster, monitoring the jobs and reporting back to the ResourceManager.
* ApplicationMaster, Runs alongside each application and negotiates the required resources from the ResourceManager, and works with the NodeManager to execute and monitor each task.
