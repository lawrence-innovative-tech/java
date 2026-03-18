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
- Broker allows replication of partitions, Partitions creates equal or below brokers. Because, Partition is copy of the message stores in brokers. 
- Brokers controls by controllers, who leader of the partitions and followers. 
- Topic is categories or Logical channels.
#### **Partition
- Producer handles partition, partition configure based on requirement each partition has one leader and follower.
- Producer instance decide which partition need to send message. If, message has key it hash(key) % Partitions to identify which partition leader received message. No key it used RoundRobinMessage or StricklyMessage technics to send message. It called Partitioner handles partition.
#### **Producer 
- Producer is application or instance. It connects kafka broker dynamically using boostrap.properties = broker1@9092,broker2@9092.
- Producer check partition metadata leader. By default 5min once, it configured in metadata.max.age.ms = 300000ms.
- Producer request to broker to fetch partitions details, partitioner decide which partition to push or publish message.
  