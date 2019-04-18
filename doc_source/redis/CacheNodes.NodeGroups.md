# Redis Nodes and Shards<a name="CacheNodes.NodeGroups"></a>

A shard \(API/CLI: node group\) is a hierarchical arrangement of nodes \(each wrapped in a cluster\)\. Shards support replication\. Within a shard, one node functions as the read/write primary node\. All the other nodes in a shard function as read\-only replicas of the primary node\. Redis version 3\.2 and later support multiple shards within a cluster \(API/CLI: replication group\) thereby enabling partitioning your data in a Redis \(cluster mode enabled\) cluster\. 

The following diagram illustrates the differences between a Redis \(cluster mode disabled\) cluster and a Redis \(cluster mode enabled\) cluster\.

![\[Image: Redis (cluster mode disabled) & Redis (cluster mode enabled) shards (API/CLI: node groups)\]](http://docs.aws.amazon.com/AmazonElastiCache/latest/red-ug/images/ElastiCache-NodeGroups.png)

Both Redis \(cluster mode disabled\) and Redis \(cluster mode enabled\) support replication via shards\. The API operation, [DescribeReplicationGroups](https://docs.aws.amazon.com/AmazonElastiCache/latest/APIReference/API_DescribeReplicationGroups.html) \(CLI: [describe\-replication\-groups](https://docs.aws.amazon.com/cli/latest/reference/elasticache/describe-replication-groups.html)\) lists the node groups with the member nodes, the node’s role within the node group as well as other information\.

When you create a Redis cluster, you specify whether or not you want to create a cluster with clustering enabled\. Redis \(cluster mode disabled\) clusters never have more than one shard which can be scaled horizontally by adding \(up to a total of 5\) or deleting read replica nodes\. For more information, see [High Availability Using Replication Groups](Replication.md), [Adding a Read Replica, for Redis \(cluster mode disabled\) Replication Groups](Replication.AddReadReplica.md) or [Deleting a Read Replica, for Redis \(cluster mode disabled\) Replication Groups ](Replication.RemoveReadReplica.md)\. Redis \(cluster mode disabled\) clusters can also scale vertically by changing node types\. For more information, see [Scaling Redis \(cluster mode disabled\) Clusters with Replica Nodes](Scaling.RedisReplGrps.md)\.

When you create a Redis \(cluster mode enabled\) cluster, you specify from 1 to 90 shards\. 

**Note**  
The node or shard limit can be increased to a maximum of 250 per cluster\. To request a limit increase, see [AWS Service Limits](https://docs.aws.amazon.com/general/latest/gr/aws_service_limits.html) and select limit type "Nodes per cluster per instance type”\. 

When you create a new cluster, as long as the cluster group has the same number of shards as the old cluster, you can seed it with data from the old cluster so it doesn’t start out empty\. This can be helpful if you need change your node type or engine version\. For more information, see [Making Manual Backups](backups-manual.md) and [Restoring From a Backup with Optional Cluster Resizing](backups-restoring.md)\.
