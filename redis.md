# Redis

Redis is a powerful, open-source, in-memory data structure store used to implement NoSQL key-value databases
- single thread
- written in C

Redis can run as a single node, with a high availability (HA) replica, or as a cluster. When operating as a cluster, Redis clients cache a set of "hash slots" which map keys to a specific node. This way clients can directly connect to the node which contains the data they are requesting.

Each node maintains some awareness of other nodes via a gossip protocol so, in limited instances, if you request a key from the wrong node you can be redirected to the correct node. But Redis' emphasis is on performance so hitting the correct endpoint first is a priority.

Redis is really, really fast. Redis can handle O(100k) writes per second and read latency is often in the microsecond range. This is completely a function of the in-memory nature of Redis.

## Use Cases
### Redis as a Cache
The most common deployment scenario of Redis is as a cache. Redis can distribute this hash map trivially across all the nodes of our cluster enabling us to scale without much fuss - if we need more capacity we simply add nodes to the cluster.

Using Redis in this fashion doesn't solve one of the more important problems caches face: the [hot key](#hot-key) problem, though Redis is not unique in this respect vs alternatives like Memcached or other highly scaled databases like DynamoDB.

### Redis as a Distributed Lock
Another common use of Redis in system design settings is as a distributed lock. Occasionally we have data in our system and we need to maintain consistency during updates
- A very simple distributed lock with a timeout might use the atomic increment (INCR) with a TTL. When we want to try to acquire the lock, we run INCR, When we're done with the lock, we can DEL the key so that other processes can make use of it.

### Redis for Leaderboards
Redis' sorted sets maintain ordered data which can be queried in log time which make them appropriate for leaderboard applications. 

### Redis for Rate Limiting
As a data structure server, implementing a wide variety of rate limiting algorithms is possible. A common algorithm is a fixed-window rate limiter where we guarantee that the number of requests does not exceed N over some fixed window of time W.

### Redis for Proximity Search
Redis natively supports geospatial indexes with commands like GEOADD and GEORADIUS.

### Redis for Event Sourcing
Redis' streams are append-only logs similar to Kafka's topics. The basic idea behind Redis streams is that we want to durably add items to a log and then have a distributed mechanism for consuming items from these logs. Redis solves this problem with streams (managed with commands like XADD) and consumer groups (commands like XREADGROUP and XCLAIM).



#### Hot Key
If our load is not evenly distributed across the keys in our Redis cluster, we can run into a problem known as the `hot key` issue.
- potential solutions
    - We can add an in-memory cache in our clients so they aren't making so many requests to Redis for the same data.
    - We can store the same data in multiple keys and randomize the requests so they are spread across the cluster.
    - We can add read replica instances and dynamically scale these with load.

## Redis Types

### Redis Sentinel
Redis Sentinel provides high availability for Redis with a system that automatically detects master node failures and replaces it with a slave node.

Key Features:
- Monitoring
- Notification
- Automatic Failover: If a master node is non-responsive, Redis Sentinel can start a failover process, promoting a slave to master.
- Configuration Provider

However, it’s worth mentioning that Redis Sentinel does not provide any sharding mechanisms. All write and read operations still go to a single master node, which could be a potential bottleneck in a large-scale system.


### Redis Cluster

Redis Cluster is a distributed version of Redis that provides a way to run a Redis installation where data is automatically sharded across multiple Redis nodes.
Key Features:
- Automatic Sharding: Data is automatically divided across multiple nodes in a Redis cluster, enabling horizontal scaling and improving performance.
- High Availability: Like Redis Sentinel, Redis Cluster also provides high availability. It can survive partitions where a majority of master nodes are reachable and at least one reachable master node exists for every hash slot.
- Read Scaling: You can scale read operations by configuring read replicas.

Redis Cluster does not use Sentinel nodes. Instead, all nodes are responsible for failover and configuration settings, which simplifies the system.

## Redis Sentinel vs Redis Cluster

`Redis Sentinel` is ideal for those who need a robust failover mechanism without the complexities of data sharding. It provides automatic master failover to a replica and service discovery to clients. It’s a great choice for applications where high availability is a priority, and all data can reside on a single Redis node.

`Redis Cluster`, on the other hand, is for use cases that need to automatically shard data over multiple nodes to achieve higher levels of scalability. If your application has large data sets that exceed the capacity of a single Redis node or high-throughput scenarios where distributing the load over multiple nodes is beneficial, then Redis Cluster is the way to go.


## References
- [hellointerview.com](https://www.hellointerview.com/learn/system-design/deep-dives/redis)
- [medium.com](https://medium.com/@chaewonkong/redis-sentinel-vs-redis-cluster-a-comparative-overview-8c2561d3168f)
