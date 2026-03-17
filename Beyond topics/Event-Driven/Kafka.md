#### **Purpose
- Kafka is Event-driven architecture to process or stream data asynchronously. 
- Kafka 2.x uses zookeeper, 3.x uses zookeeper and kraft, 4.x uses only kraft.

#### **Zookeeper and KRaft Responsibility
- Maintain List of topics.
- Decide leader of the partition and followers.
- Controls cluster metadata and brokers.

#### **Zookeeper
- Zookeeper externally communicates kafka cluster, controllers cluster metadata, broker details, leader elections.
- Zookeeper election using Consensus + Atomic protocols. Each request send it to followers in order. Atomic protocol decide the who is next leader if exist one dead.

#### **KRaft
- Kafka Raft is a consensus algorithm to manages metadata of controllers.
- Consensus protocol leader elections, the leader broadcast to every followers in certain time period