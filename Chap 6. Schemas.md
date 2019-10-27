## Chapter 6 Schemas

### Schema technologies capabilities

* Multiple schema languages, some technologies give you multiple options for a given data type.
* Validation rules, some technologies go further than data types by letting you express validation rules on an events properties.
* Code generation, schema technologies often support code generation, which will generate idiomatic classes or records in your preferred language from the schema.
* Multiple encodings, some schema technologies allow you to encode and decode records in multiple formats, eg. Binary or Human Readable format.
* Schema evolution, versioning and schema evolution gives the ability to evolve with the business and data evolution.

### Schemas

* Apache Avro, is an RPC and data serialization system that was developed as part of the Apache Hadoop project. Avro has a declarative JSON-based schema language for describing data types. Avro has two representations for data; a compact binary encoding and a human-readable JSON encoding.
* Apache Thrift, framework for cross-language services development. Has its own definition language that allows you to define data types as well as service interfaces.
* JSON Schema, is a declarative language written in JSON. JSON Schema doesn't specify the data serialization only how to define data types. JSON schema provides rich validation rules for its schema data types. JSON is often the default schema used by immature business teams as the format is human readable.
* Protocol Buffers, schema technology and data serialization mechanism from Google. Supports protocol definition syntax that lets the user define data structure in .proto files.

### Summary

* A unified log is a decoupled architecture; consumers and producers of event streams ahve no particular knowledge of each other.
* The contract between event consumers and producers is represented by the schema of each event.
* We need a way to associate events with their schemas; either one stream per schema, trial and error, or self describing events.
* A schema registry is a central repository for all of our schemas; this is the source of truth for which schemas are available as part of our company's unified log.
