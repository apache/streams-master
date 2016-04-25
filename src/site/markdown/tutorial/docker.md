## Set up a local environment to run streams

First of all, you do not run 'Streams' as software.  Rather, you run 'streams' which use Streams components and libraries under the cover.

Streams components can be embedded in a variety of data processing frameworks based on the problem and performance requirements at hand.

A great way to get started collecting and indexing data is with streams-runtime-local and Docker.

### Confirm Docker is healthy

We'll assume you've got docker up and running.

Run from your command line:

> $ docker ps
  
If you see a (possibly empty) list of running containers, you are good.

