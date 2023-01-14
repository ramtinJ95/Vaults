### Notes
+ The unit of data in Kafka is a message. Think of it as a row in a table. A message can have some optional piece of data, metadata, which is called a key. Keys are used when messages are to written to partitions in a controlled manner
+ Kafka devs prefer Apache Avro for message schemas since it has many structural features that Json lacks
+ Messages are categorised into topics. Think of them as tables/folders. Each topic can have several partitions. There is no guarantee of message ordering across an entire topic, only within each partition.
+ A single Kafka server is called a broker. The broker gets messages from producers assigns offsets to them and writes the message to disk.
+ page 28. talks about how to chose number of partitions for a topic
+ page 30-32 talks about retention periods and volume
+ Having more memory available to the system for page cache will improve the performance of consumer clients. Reason for this is that consumer can read the data from page caches instead of waiting for the broker to fetch data from disk. Thus it is important that Kafka is not colocated with another application on a system, so that it does not share the use of the page cache.
+ Having a singel Kafka broker in production is not recommended due to risk of data loss in case of system failure. Also with multiple servers i.e broker the ability to scale and share the load is always there.
+ Very interesting point on how to tune even the OS to increase performance of the Kafka process on page 38-39
+ Keep use of Zookeeper minimal as the Kafka project is moving towards deprecating it.
+ Kafka uses its own hashing algorithm so that values dont change if java versions change something with their hash algo. Brilliant! I have to check if this is true for our dbt hashing stuff.
+ If new partitons are added after the fact, you cannot be use that messages that used to end up in partition X will keep going there. Thus is it recommended to never add partitions to a topic after its already been published to. 
+ Headers of a record gives the ability to add some metadata about the Kafka record, without adding any extra info to the key/value pair of the record itself. Headers are often used for lineage to indicate source of the data record. 
+ Kafka consumers can be in consumer groups. A group of consumers that read from a topic, all share the partitions between them. That is P1 goes to C1 and P2 goest to C1 but P3 goes to C2. There is no point inn having more consumers than partitions because it will lead to idle consumers.
+ It's possible and even useful to have multiple consumer groups read from the same topic. In this way many applications can see everything that gets published to a topic. This will not really impact Kafka's performance since it was developed with this use case in mind.
+ When adding a new consumer to a consumer group, there will be some rebalancing that happens regarding which consumer consumes from which partition.
+ There are two rebalancing strategies
	+ Eager rebalancing: When a new consumer joins, everything stops in the consumer group and every consumer will get a new partition to read from
	+ Cooperative rebalancing: Reassigns only a subset of the partitions from one consumer to another and this allows consumers to keep proccessing the other partitions and thus avoids the total stop
+ Consumers maintain membership in a consumer group by sending heartbeats to a kafka broker assigned as the group coordinator. Every time a consumer stops being alive either by being scaled down or crashing, there will be a rebalancing that happens. 
+ Static group membership means that when a consumer joins it is assigned partitions as normal. But when this consumer goes down and rejoins, it will get back exactly those partitions it had, i.e no rebalancing happens. This is useful if the application maintains local state or a cache that is populated by the partitions which is assigned to the consumer. When re-creating this cache is time consuming, we dont want this re-creating to happens every time something happens to this consumer
+ Thread safety: You can have multiple consumer that belong to the same group in one thread, and you cant have multiple threads safely use the same consumer. One consumer per threads is the rule. Page 87 have many links to blog posts that goes into more detail
+ consumer assignment strategy is explained page 91.
+ Re-balancing of consumer groups can lead to duplicate or lost data, because of how commit offsets are handled. Read more on page 94-96
+ If you want only one consumer there are some subtle differences in setup that is worth keeping mind see page 110.
+ If we ever want to use kafka adminclient read chapter 5 i skipped entirely.
+ Data in Kafka is organised by topics. Each topic is partitioned and each partition can have multiple replicas. Those replicas are stored on brokers and each broker typically stores hundreds even thousands of replicas belonging to different topics and partitions.
+ Usually follower replicas dont serve client requests. But in more recent versions this is allowed given that the replica is in sync with leader replica. 
+ Compaction is a quite central concept in Kafka it also determines how much memory is needed for storage of old messages. Read more page 156
+ Deleted events section page 158 with the compaction stuff is very important for our use case at menti
+ Replication configs are on page 165
+ Scenarios where data loss is possible even with a good replication schema is very well explained on page 169-170
+ Important consumer configuration properties for Reliable processing are discusson page 173-174
+ Validate system relability. Do it in 3 layers; validate the config, validate the applicaiton and monitor the app in production.page 176-178 has very good examples and tips.
+ Limitations of the idempotent producers are quite sever and worth keeping in mind in case one wants to have "exactly once" semantics. page 184-185.
+ Important to remember that transactions in Kafka were developed specifically for stream processing applications. Therefor they where build to work the "consume-process-produce" pattern that forms the basis of stream processing applications. 
+ For "exactly once" semantics we have to configure isolation levels on the consumer too. This is very well explained 189-192
+ Microservices often need to update the database and publish a message to Kafka within a singel atomic transaction. Kafka transaction will not do this. A common solution to this common problems is know as the "outbox pattern". The Debezium project as in-depth blog posts on this pattern.
+ For CDC with Kafka use Debezium connectors. Also read the Debezium docs since they have great blog posts and patterns to follow imbedded in their dev docs. 
+ Before starting to use Kafka connect its smart to re-read chap 9. Especially page 226-229.

### Jobb specific notes
+ Look into using Kafka as tracking-api replacement. As it was developed for a similar use case to being with.
+ Think about how much throughput and latency we want our new data systems to guarantee.
+ Look into tiered storage stuff for Kafka. Could be quite useful for us.
+ Tracking-api having issues with duplicate events is because its an "at least once" system and not an "exactly once" system. It probably has to do with the retry mechanism in core and within tracking-api
+ We should add an event-id to tracking events so we can guarantee uniqueness. Primary use case at job for Kafka will be satisfied by using the Kafka connect-api. see page 214.