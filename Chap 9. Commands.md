## Chapter 9 Commands

* A command is an order or instruction for a specific action to be performed in the future.
* Each command when executed produces an event.
* Representing command explicitly as one or more event streams in the unified log is a powerful processing pattern.

### Reasons for command separation

* It makes decision code simplier. make_decision(obj) only needs to emit a command, it doesn't need to be coupled with the logic of how to respond to that command.
* Decision making code is more DRY, flexible, easier to test and auditable.
* Within a unified log environment it is easier to replay a list of commands.

### Pattern structure

* Source event stream, you would have a decision making application listening to one or more source event streams. The application would need to implement an interface make_decision(obj). The output of the application is to push commands onto the command event stream.
* Command execution application would listen on the command event stream and would execute the commands. It would then push the executed commands events onto the executed commands event stream.

### Modelling commands

* Shrink wrapped, the command must contain everything that could possibly be required to execute the command; the executor should not need to look up additional information to execute the command.
* Fully baked, the command should define exactly the action for the executor to perform; we should not have to add business logic into the executor to turn each command into something actionable.

### Scaling commands

There is multiple options for scaling to processing hundreds/thousands of commands:

* One stream per command.
* Commands are self describing, write each command to 3/5 streams where each stream represents a certain priority.
* Commands are self describing and have a single stream. Include a header in each record that tells the command executor what type of command it is.

When scaling up an implementation of commands in your unified log, consider how many command streams to operate, how to handle execution failures and whether to implement command hierarchies.
