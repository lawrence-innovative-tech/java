#### **Purpose
- Kafka is Event-driven architecture to process or stream data asynchronously. 
- Kafka 2.x uses zookeeper, 3.x uses zookeeper and kraft, 4.x uses only kraft.
- Kafka order Grantee.
- Create replication. Factor <= broker count.
#### **Zookeeper and KRaft Responsibility
- Maintain List of topics.
- Decide leader of the partition and followers.
- Controls cluster metadata and brokers.
#### **Zookeeper
- Zookeeper externally communicates kafka cluster, controllers cluster metadata, broker details, leader elections.
- Zookeeper election(ZAB - Zookeeper Atomic Broadcast) using Consensus + Atomic protocols. Each request send it to followers in order. Atomic protocol decide the who is next leader if exist one dead.
#### **KRaft
- KRaft controls in defined control nodes, A node may have two roles one brokers and controllers or combined. It inside kafka.
- Kafka Raft is a consensus algorithm to manages metadata of controllers.
- Consensus protocol leader elections, the leader broadcast to every followers in certain time period. Every followers wait next time heartbeat if not received heartbeat within time calculate by followers it assumes leader is dead. Now, the followers become candidate sends RequestVote RPC protocol to every followers with last log term, now every followers checks two condition, who has latest lastlogterm and if equal or not lastlogindexterm. If yes reply "Yes" or "No". So, each controllers response of the election request.
#### **Broker
- Broker is data worker or Storage. Stores all the messages from producer and deliver to consumers.
- Broker allows replication of partitions.
- Broker has only leader partition and follower in other replicas.
- Brokers controls by controllers, who leader of the partitions and followers. 
- Topic is categories or Logical channels.
#### **Partition
- Controller creates partition if configured. Broker holds topics and partitions.
- Never creates partition beyond broker because each broker should hold one partition of each topic either leader or follower.
- Partitioner in producer instance it decide which partition to send message, so if message send with key using hash(key) % list of leader partitions. if no key default raft use Strick message partition. it send message one partition when it reach time or storage based limit.
#### **Producer 
- Producer is application or instance. It connects kafka broker dynamically using boostrap.properties = broker1@9092,broker2@9092.
- Producer check partition metadata leader. By default 5min once, it configured in metadata.max.age.ms = 300000ms.
- Producer request to broker to fetch partitions details, partitioner decide which partition to push or publish message.

#### **Consumer group
- Each topics may have multiple consumer group can process the same records.
- Each consumer group has own _\_committed-offset_, so it may process same records in each group. So, creates group different functionality and different process effectively.
- Each topics has one consumer group consumer are register in consumer group.
- Group co-ordinate (broker any broker become) handles specific consumer group. Co-ordinate assign as group leader. That group leader instruct to consumer connects partition leader directly.
- Consumer is application or instance. Each consumer connects through TCP. 
- Consumer checks time frequently not push notification like. because of TCP connection.
- Each consumer connects exactly connect only one partition leader so, beyond of consumer waste. eight consumer <= partition.
- Consumer use by default technics is cooperative sticky.
#### **Rebalancing
- Kafka guarantee each consumer group each consumer connects only one partition at a time.
- Consumer group listen consumer heartbeat, when add new consumer or leaves or crashed, and new partition added kafka consumer group decide to re-distribute partition to consumer, These consumer follows committed offset value to continues the process. 
#### **Offset
- Each partition has offset, this offset maintains consumed record in the kafka.
- offset start with 1.
- Offset concept really helps to maintain continues after crashes, restarted or rebalanced.
#### **Committed offset
- Stores offset value in kafka side so, guarantee to new consumer start process to current offset value.
- **Current offset -** maintain by consumer locally.


  