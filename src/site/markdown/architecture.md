##Architecture

Streams contains libraries and patterns for specifying document schemas and converting documents to and from ActivityStreams format, and runtime bindings for deploying, monitoring, and interfacing with running streams.

In general streams can be characterized as perpetual (capable of running indefinitely) or non-perpetual (expected to run until all providers run out of data).

###Basic Concepts

####Activity

Apache Streams has a preference for ActivityStreams formatted messages.  These messages may be passed using the 'Activity' class or one of it's sub-classes.  

####Datum

A Datum is a single piece of data within a stream.  A datum typically has an identifier, a timestamp, a document (which may be any java object), and additional metadata kept apart from the document related to upstream or downstream processing..

####Module

Apache Streams consists of a loosely coupled set of modules with specific capabilities.  Such as:
 * collecting data.
 * transforming or filter data
 * storing and retrieving documents and metadata from databases
 * binding streams components to other systems
 * facilitating starting and stopping of streams.

Each module has it's own POM and dependency tree.  Each stream deployment needs to import only the modules it needs.

####Pipeline

A Pipeline is a set of collection, processing, and storage components structured in a directed graph (cycles may be permitted) which is packaged, deployed, started, and stopped together.

####Runtime

A Runtime is a module containing bindings that help setup and run a pipeline.  Runtimes may submit pipeline binaries to an existing cluster, or may launch the processes to execute the stream directly.  
####Schema

A Schema defines the expected shape of the documents that will passed from step to step within a stream.  Defining the schema for a type of document allows source files and resource files to be generated at compile time. Schema can include other schemas, whether in the same repo or available via HTTP, allowing for full or partial reuse.

####Component

Components are individual instances of classes that do stuff within a stream.  Components are assembled into pipelines and executed using a runtime.  

####Types of Components

#####Provider

A Provider is a component that *provides* data to the stream from external systems.

#####Processor

A Processor is a component that *processes* data flowing through the stream - transformations, filters, and enrichments are common processors.

#####PersistWriter

A PersistWriter is a component that writes data exiting the stream.

#####PersistReader

A PersistReader is a component that reads data, often previously written by a PersistWriter.
