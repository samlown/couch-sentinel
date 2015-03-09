# Quorumify

Automated monitoring, failure detection, and master selection. With similar objectives to [Redis Sentinel](http://redis.io/topics/sentinel), Quorumify is a generic solution to maintain a master host configuration detail in systems with a potential single point of failure.

Changes can be either requested manually or as a result of fault detection. A quorum algorithm decides which host should be the master before allowing a configuration detail to change. Communication is handled by ZeroMQ using PUB/SUB sockets to efficiently transmit heartbeats between multiple servers and elect a new master in the case of failure.

There are several parts to Quorumify:

 * `quorumify-server` reads a configuration file and periodically sends out heartbeats to anyone subscribed. In turn, the process listens for incoming heartbeats and attempts to suggest an alternate host in the case of failure or when requested.
 * `quorumify-client` subscribes to servers and waits for events decided by a quorum. If a change occurs, the configuration file determines what actions should be taken.
 * Client libraries subscribe to quorumify servers using ZeroMQ SUB sockets and wait for incoming changes that prompt some kind of action specifically programmed in the library. The Quorumify protocol is sufficiently simple for your own libraries to be implemented easily.


## Configuration

Quorumify accepts a simple YAML configuration file the describes the environment.
