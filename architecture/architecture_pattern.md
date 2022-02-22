# Architecture Pattern
Multiple styles for a Component and Connector architecture exists and usage depends
on the specification of the project

1. **Data Flow Styles**
  - Computation model in which components act as data transformers and
  connectors transmit data from the output of a component to the input
  of another one. Component's job is to consume data on its input ports
  and write transformed data to its output ports. Used in stream processing
  application.
  1. Pipe-and-Filter Style
     - Data arrives at a filter's input ports, is transformed, and then is 
     passed via its output ports through a pipe to the next filter
     - Filter -> Component that transforms data
     - Connector -> UNIX style pipe

2. **Call-Return Styles**
  - Computational model in which components provide a set of services that
  may be invoked by other components.
  - Component -> invoking a service pauses until that service has completed
  - Connectors -> conveying the service request from the requester to the provider
  and for returning any results.
  1. Client-Server Style
    - Components interact by requesting services of other components asymmetricly
    - Service invocation is synchronous since the requester is block until it receives
    an answer
    - Components:
      - Clients -> Ports that describe the services they require 
      - Servers -> Provides service to client and may act as a client
    - Connector -> Request/Reply connector used for invoking services.
  2. Peer-to-Peer Style
    - Components directly interact as peers by exchanging services.
    - Removes the asymmetry of Client-Server since any components can interact with any
    other component
    - Two way communication
    - Connector -> call-return connector
  3. Service-Oriented Architecture Style
    - Collection of distributed components that provide and/or consume services.
    - Service provider components and service consumer components can use different impl.
    languages and platforms
    - Services are standalone and deployed independently

3. **Event-Based Styles**
  - Allows components to communcate through asynchronous messages often call Pub Sub systems 
