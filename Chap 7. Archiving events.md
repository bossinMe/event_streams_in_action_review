## Chapter 7 Archiving events

* A unified log is not designed as a long term store of events.

### Trim horizon/Retention period

* Kafka/Kinesis both have a limit on how long it will hold onto logs for. The retention period is the amount of time that a log will be held onto before being delete from the kafka stream.
* The log retention allows for streams to be replayed from a particular offset.

### Resilience/Reprocessing/Refinement

* Although the retention period allows you to replay logs from a particular offset. It requires that downstream errors be fixed before the retention period ends.
* To improve resilience we can add in a stream sink to store the raw events of the stream into a long term storage to allow for replaying streams longer than the kafka/kinesis retention period. You could have a producer that pulls from the log sink and pushes the events straight back into Kafka/kinesis.
* Assuming that the downstream consumers are bug free, replaying streams may not produce the same results. Late-arriving data usually doesn't have the same value as real time. Approximation, you may choose to approximate stream processing calculations  for performance reasons. The stream processing framework may have limitations on processing/replaying a log stream.

### Archiving

* You should be archiving the events as close to the source as possible.
* The events should be stored into a redundant, distributed, low cost, long term storage solution.
* Archiving usually takes the following steps, read events from the stream, batch up events into a suitable file that is optimized for subsequent data processing and write the file to the storage solution.
