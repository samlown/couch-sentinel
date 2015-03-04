# Couch Sentinel

Automatic connection failover for CouchDB. With similar objectives to [Redis Sentinel](http://redis.io/topics/sentinel), Couch Sentinel will help you maintain a configuration of CouchDB servers replicating each other, monitor them for issues, determine which should be the master, and automatically push a new configuration to proxies (`dbproxy`) via ZeroMQ.

The tool is split into two applications:

 * `sentinel`, reads in a configuration file, sets up a ZeroMQ PUB socket, and starts polling the couchdb servers for issues. If something goes wrong, it'll try to decide what to do.
 * `dbproxy`, subscribes to the sentinel's PUB socket, and prepares to relay incoming requests to the current master.


## Configuration

Sentinel accepts a simple YAML configuration file the describes the CouchDB environment.

