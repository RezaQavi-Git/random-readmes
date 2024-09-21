

# Sharding
Sharding is a method for distributing data across multiple machines. MongoDB uses sharding to support deployments with very large data sets and high throughput operations.

There are two methods for addressing system growth: vertical and horizontal scaling.
- Vertical Scaling involves increasing the capacity of a single server, such as using a more powerful CPU, adding more RAM, or increasing the amount of storage space. 
- Horizontal Scaling involves dividing the system dataset and load over multiple servers, adding additional servers to increase capacity as required. While the overall speed or capacity of a single machine may not be high, each machine handles a subset of the overall workload, potentially providing better efficiency than a single high-speed high-capacity server.


# MongoDB sharded cluster Infrastructure

## Router Servers
- Provides the interface between the client applications and the sharded cluster.
- Route queries and write operations to the shards.
- Behaves identically to any other MongoDB instance from the perspective of the application.

## Config Servers
- Stores the metadata for a sharded cluster. The metadata reflects state and organization for all data and components within the sharded cluster. The metadata includes the list of chunks on every shard and the ranges that define the chunks. The mongos instances cache this data and use it to route read and write operations to the correct shards. mongos updates the cache when there are metadata changes for the cluster, such as Chunk Splits or adding a shard. Shards also read chunk metadata from the config servers.
- Stores Authentication configuration information such as Role-Based Access Control or internal authentication settings for the cluster.
- MongoDB also uses the config servers to manage distributed locks.
- Each sharded cluster must have its own config servers. Do not use the same config servers for different sharded clusters.

## Shard
- Contains a subset of sharded data for a sharded cluster. Together, the cluster’s shards hold the entire data set for the cluster.
- Users, clients, or applications should only directly connect to a shard to perform local administrative and maintenance operations.
- Performing queries on a single shard only returns a subset of data. Connect to the mongos to perform cluster level operations, including read or write operations.

To keep it minimal we will deploy a Router, a Config Server, two Shards containing 3 instances each with a Primary-Secondary-Secondary replica set.

# Shard Keys
MongoDB uses the shard key to distribute the collection's documents across shards. The shard key consists of a field or multiple fields in the documents.

## Choose a Shard Key
The choice of shard key affects the creation and distribution of chunks across the available shards. The distribution of data affects the efficiency and performance of operations within the sharded cluster.

The ideal shard key allows MongoDB to distribute documents evenly throughout the cluster while also facilitating common query patterns.

When you choose your shard key, consider:
- the cardinality of the shard key
    - The cardinality of a shard key determines the maximum number of chunks the balancer can create. Where possible, choose a shard key with high cardinality. A shard key with low cardinality reduces the effectiveness of horizontal scaling in the cluster.
- the frequency with which shard key values occur
    - The frequency of the shard key represents how often a given shard key value occurs in the data. If the majority of documents contain only a subset of the possible shard key values, then the chunks storing the documents with those values can become a bottleneck within the cluster. Furthermore, as those chunks grow, they may become indivisible chunks as they cannot be split any further. This reduces the effectiveness of horizontal scaling within the cluster.
- whether a potential shard key grows monotonically
- Sharding Query Patterns
    - In a sharded cluster, the mongos routes queries to only the shards that contain the relevant data if the queries contain the shard key. When the queries do not contain the shard key, the queries are broadcast to all shards for evaluation. These types of queries are called scatter-gather queries. Queries that involve multiple shards for each request are less efficient and do not scale linearly when more shards are added to the cluster.
- Shard Key Limitations


## Chunks
MongoDB partitions sharded data into chunks. Each chunk has an inclusive lower and exclusive upper range based on the shard key.

### Balancer and Even Data Distribution
In an attempt to achieve an even distribution of data across all shards in the cluster, a balancer runs in the background to migrate ranges across the shards.

# Advantages of Sharding
- Reads / Writes
    MongoDB distributes the read and write workload across the shards in the sharded cluster, allowing each shard to process a subset of cluster operations. Both read and write workloads can be scaled horizontally across the cluster by adding more shards.

- Storage Capacity
    Sharding distributes data across the shards in the cluster, allowing each shard to contain a subset of the total cluster data. As the data set grows, additional shards increase the storage capacity of the cluster.

- High Availability
    The deployment of config servers and shards as replica sets provide increased availability.

`Once a collection has been sharded, MongoDB provides no method to unshard a sharded collection.`
