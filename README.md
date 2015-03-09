# Quorumify

Automatic failure detection and master selection. With similar objectives to [Redis Sentinel](http://redis.io/topics/sentinel), Quorumify is a generic solution to help you maintain connection configuration details and push changes to clients as manual requests or in the event of a system failure. Communication is handled by ZeroMQ using PUB/SUB sockets to efficiently transmit heartbeats between services and elect a new master in the case of failure. 

There are two parts to quorumify:

 * `quorumify`, the main server application that reads in a configuration file, sets up ZeroMQ PUB/SUB sockets, and starts listening out for incoming messages.
 * `dbproxy`, subscribes to the sentinel's PUB socket, and prepares to relay incoming requests to the current master.


## Configuration

Sentinel accepts a simple YAML configuration file the describes the CouchDB environment.

