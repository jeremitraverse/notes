# Publish subscribe 

### AMQP (Advance Message Queuing Protocol)
  - Primary used by RabbitMQ 
  - Main functionnalies:
    - Message orientation 
      - Round robin
    - Queues: 
      - Producer -> Generating messages that are being sent to broker
      - Broker -> Handles the exchanges and queues
        - Binding : Binds an exchange to a queue
        - Exchange : 
          - Direct exchange : exchange check the routing_key and try to match it with a binding
          that has the same routing_key 
          - Default exchange : Same concept to direct exchange, but all the default_queues are
          attatched to the default_binding. By default, all the queues are attached to the 
          default_binding
          - Topic based exchange : Default exchange but handles tokens -> wildcards 
            (# -> 1 .. 1000 motes, + -> 1 .. 1 mot)
          - Fanout : No routing_key identification (1 -> N)
          - Headers exchange : Same has topic base but can handle multiple topics at the same time 
    - Routing fiability
    - Very secure
    - A subscriber can create it's own queue

