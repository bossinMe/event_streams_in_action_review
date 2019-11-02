## Chapter 8 Railway-oriented processing

* Log processing needs to build into fault tolerance and fault handling to degrade gracefully with errors.
* Given enough events all bugs are inevitable.

### Unix

* Unix has 3 standard streams.
  1. Stdin, the input stream of data going into a Unix program.
  2. Stdout, The output stream where a unix program writes data related to successful operation.
  3. Stderr, The output stream where a unix program writes data related to failed operation.
* A unix process that ends up failing with a nonzero exit code may well also write output to stdin before it fails.
* A unix process may write warnings or diagnostic output to stderr before ultimately returning with a zero code indicating success.
* Composable, we can combine multiple successes and failures, and the combined result will still make sense. eg. false | true | echo $?
* By default the unix pipe will only output the last program return code.
* 'set -e' will terminate the script as soon as any command within the script returns a nonzero error code.

### Failure and the unified log

* "Reports that say that something hasn't happened are always interesting to me, because as we know, there are known knowns; there are things we know we know. We also know there are known unknowns; that is to say, we know there are some things we do not know. But there are also unknown unknowns - the ones we don't know we don't know." US Secretary of Defense Donald H. Rumsfeld.

#### Failure path

* Our failure path must not be out-of-band. We don't need to rely on third-party logging tools; we are implementing a unifed log, so let's use it.
* Entries in our failure path must contain the reason or reasons for the failure in a well-structured form that both humans and machines can read.
* Entries in our failure path must contain the original input data, so that the unit of work can potentially be replayed if and when the underlying issue can be fixed.

### Happy and unhappy paths

* We can design our process to look very similar to a unix process. 3 streams, one input stream, one output stream for successful processing and one output stream for failure processing.
* We have done away with exit values. The success and failure of a given unit of work is reflected in whether output was written to the success or failure output stream.
* We have removed any any ambiguity in the outputs. A unit of work results in output either to the happy stream or the failure stream, never both, never neither.
* We are using the same in-band tools to work with both our successes and our failures. Failures will end up as well-structured entries in one event stream; successes will end up as well-structured entries in the other event stream.

### Failure event

* The failure event structure will look something very similar to the successful entry. Subject, verb, direct object, timestamp and the original event.

### Railway oriented approach

* It composes failures within an individual processing step, but it fails fast across multiple steps.
* The type inside our 'Success' can change between each processing step.
* The type inside our 'Failure' must stay the same between each processing step.

### Summary

* Composition in the large, we compose multiple event-stream-processing workflows out of multiple stream-processing jobs, each of which outputs a happy stream and a failure stream.
* Fail fast as the filling or patty, when processing multiple work steps we want to fail at the first step that fails.
* Composition in the small, if we have multiple independent steps we can use composition at the end to work out if the final output should be success or failure.
