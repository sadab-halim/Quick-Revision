<img src="https://r2cdn.perplexity.ai/pplx-full-logo-primary-dark%402x.png" style="height:64px;margin-right:32px"/>

# You are an Apache Kafka expert and mentor.

Your task is to generate a structured **quick revision guide** on Kafka, broken into sections.  
I will specify which section to start from, and you will cover ONLY that section in detail.

### Output Rules:

- Be concise, exam-friendly, and clear.
- Use headings, bullet points, tables, and short command/code snippets.
- Highlight **common pitfalls**, **best practices**, and **Kafka version notes** (esp. KRaft, Tiered Storage).
- Use comparison tables where useful (e.g., Kafka vs traditional messaging, consumers vs consumer groups).
- Include **short real-world examples** (Java/Spring Boot Kafka code, CLI commands, configs).
- For complex or abstract topics (e.g., partitions, consumer groups, replication, event streaming), use **real-life analogies** to simplify learning.
- End each section by asking if I want to continue with the next one.


### Sections:

1. Introduction to Kafka
What is Apache Kafka?
Kafka as a Distributed Streaming Platform
Kafka vs Traditional Messaging Systems (RabbitMQ, ActiveMQ, etc.)
Use Cases: Messaging, Event Sourcing, Log Aggregation, Stream Processing
Core Concepts: Broker, Topic, Partition, Offset
Kafka as a Distributed Commit Log
2. Kafka Architecture
Brokers and Clusters
ZooKeeper (legacy) vs KRaft (Zookeeper-less mode)
Leader Election and ISR (In-Sync Replicas)
Controller Node and Partition Reassignment
High Watermark and Committed Offsets
Cluster Metadata Management
Request Processing Flow in Kafka
3. Kafka Topics and Partitions
Topic Creation \& Configuration
Partition Count and Replication Factor
Partition Reassignment and Balancing
Log Segmentation and Retention
Cleanup Policies: Delete vs Compact
Time-based vs Size-based Retention
Log Compaction Internals
Min In-Sync Replicas (min.insync.replicas)
4. Kafka Producers
Kafka Producer API
Keyed vs Keyless Records
Partitioning Strategies (default, key-based, custom partitioner)
Acknowledgement Modes (acks = 0, 1, all/-1)
Batching and Linger.ms
Compression (Snappy, GZIP, LZ4, ZSTD)
Idempotent Producers
Transactions \& Exactly-Once Semantics (EOS)
Asynchronous vs Synchronous Send
Producer Interceptors
Error Handling \& Retries
5. Kafka Consumers
Kafka Consumer API
Consumer Groups
Polling Model and max.poll.* configs
Rebalancing Strategies: Range, Round Robin, Sticky, Cooperative Sticky
Offset Management (Auto/Manual Commit)
Assign vs Subscribe APIs
Consumer Lag and Backpressure
Consumer Interceptors
Error Handling (Dead Letter Topics, Retry Topics)
6. Kafka Delivery Semantics
At-most-once
At-least-once
Exactly-once Semantics (EOS)
Transactions and Idempotence
Atomic Writes Across Multiple Partitions/Topics
Limitations and Tradeoffs
7. Kafka Configuration \& Tuning
Broker Configs (server.properties)
Producer and Consumer Tuning Parameters
Topic-level Configurations
Tuning for Performance, Latency, and Throughput
OS, JVM, and Disk Tuning for Kafka
8. Kafka Internals
Storage Structure and Log Segments
Indexes and File Compaction
Page Cache and Zero-Copy Transfer
Flush Policies and fsync behavior
Log Cleaner Threads
Leader/Follower Synchronization
ISR Shrink/Expand Behavior
9. Kafka Streams API
KStream, KTable, GlobalKTable
Stateless Operations (map, flatMap, filter, branch)
Stateful Processing (count, reduce, aggregate)
Joins (KStream-KStream, KStream-KTable, KTable-KTable)
Windowed Aggregations: Tumbling, Hopping, Sliding, Session
Handling Out-of-Order Events and Grace Periods
Fault Tolerance and State Stores (RocksDB, in-memory)
Repartition Topics and Internal Topics
Interactive Queries
Suppression in Windowed Aggregations
Processor API vs DSL
Exactly-once Processing in Kafka Streams
Scaling Kafka Streams Applications
10. Kafka Connect
Introduction to Kafka Connect
Source and Sink Connectors
Distributed vs Standalone Mode
Common Connectors (JDBC, Elasticsearch, S3, Debezium)
SMTs (Single Message Transforms)
Dead Letter Queue Support
Offset Management and Resilience
11. Schema Management
Avro, JSON Schema, Protobuf Support
Schema Registry Integration with Producers/Consumers
Schema Versioning and Compatibility Modes: Backward, Forward, Full
Field Additions, Deletions, Defaults
Enum and Nested Schema Changes
Best Practices for Schema Evolution
12. Kafka Security
Encryption (TLS)
Authentication (SSL/SASL)
SASL Mechanisms: PLAIN, SCRAM, GSSAPI (Kerberos), OAUTHBEARER
ACLs and Role-Based Access Control (RBAC)
Kafka Audit Logging and Secret Management
13. Monitoring and Observability
Key Metrics: Lag, Throughput, ISR, Partition Count
Producer/Consumer/Broker JMX Metrics
Prometheus \& Grafana Dashboards
Tools: Confluent Control Center, Kafka Manager, Burrow, Cruise Control
Log Analysis and Debugging
14. Kafka in Production
Partitioning and Replication Strategies
ISR and Replica Placement
Rolling Upgrades and Downtime Minimization
Handling Message Backlog and Lag
Retention and Compaction Tuning
Zero-Downtime Cluster Expansion
15. Kafka Performance Optimization
Producer Throughput Tuning (batch.size, linger.ms, compression)
Consumer Tuning for High Poll Volumes
Thread Pool Management in Processing Apps
Broker I/O Optimization
Page Cache Usage and OS tuning
16. Spring Boot with Kafka
KafkaTemplate and MessageListenerContainer
Spring Retry and Error Handling
Transaction Support in Spring Kafka
Dead Letter Topics and Retry Topics
Schema Registry Integration
Declarative Kafka Config via YAML/Properties
17. Integration Patterns
Event-Driven Architecture with Kafka
Event Sourcing
CQRS with Kafka and Kafka Streams
Request-Reply Pattern over Kafka
Choreography vs Orchestration in Microservices
CDC (Change Data Capture) with Kafka and Debezium
Outbox Pattern
18. Cloud \& Kubernetes Deployments
Kafka on AWS MSK, Azure Event Hub, GCP Pub/Sub (Kafka-compatible APIs)
Kafka on Kubernetes with Strimzi
Helm Charts and Operators
Networking Considerations in Cloud/K8s
Kafka in Service Mesh (Istio, Linkerd)
19. KRaft Mode (No ZooKeeper)
Metadata Quorum Controller
Migration from ZooKeeper to KRaft
Pros/Cons and Operational Differences
Current Status and Production Readiness
20. Tiered Storage
Introduction and Use Cases (KIP-405)
Local vs Remote Storage Model
Impact on Retention and Cost
Performance Implications
21. CI/CD \& DevOps
Kafka in GitOps and CI/CD pipelines
Terraform + Helm for Infrastructure as Code
Testing Kafka Configurations and Topologies
Canary Deployments with Kafka
22. Real-Time Analytics
Kafka + Apache Flink for Stateful Stream Processing
Kafka + Apache Spark Structured Streaming
Kafka + Apache NiFi for ETL
Kafka + Druid / Pinot / Elasticsearch
Kafka + BigQuery / Snowflake for Warehousing
23. Disaster Recovery \& High Availability
Cross Data-Center Replication with MirrorMaker 2
Data Backups and Snapshots
Partition Reassignment Tools
Recovery from Corrupted Topics/Segments
24. Kafka Client Ecosystem
Java, Python (Confluent, aiokafka), Go (sarama), Node.js
Kafka CLI, Confluent CLI
Client Configuration and Debugging Tools

### Instruction:

When I say **"Start from Section X"**, generate the revision guide for that section only.  
When done, ask me if I want to continue with the next section.  
Always maintain the same style so the entire revision guide feels consistent.

I am ready to begin generating your Apache Kafka revision guide. Please specify which section you would like to start with.

---

# Start from Section: Introduction

Apache Kafka is a distributed event streaming platform used for building real-time data pipelines and streaming applications. It is horizontally scalable, fault-tolerant, and capable of handling trillions of events per day.

### What is Kafka?

Kafka is fundamentally a distributed, append-only commit log. It allows applications to:

* **Publish (write)** and **subscribe to (read)** streams of events, similar to a message queue.
* **Store** streams of events durably and reliably for as long as you need.
* **Process** streams of events in real-time or retrospectively.

This combination of capabilities makes it more than just a messaging system; it's a complete streaming platform.

**Analogy:** Think of Kafka as a central nervous system for a company's data. Different parts of the organization (applications, services) can send data (nerve signals) to this central system, and other parts can react to those signals in real-time.

### Kafka vs. Traditional Messaging Systems

Kafka's design differs significantly from traditional message brokers like RabbitMQ or ActiveMQ.


| Feature | Apache Kafka | Traditional Brokers (e.g., RabbitMQ) |
| :-- | :-- | :-- |
| **Model** | **Pull-based**. Consumers pull data from brokers at their own pace. "Dumb broker, smart consumer." | **Push-based**. The broker pushes messages to consumers. "Smart broker, dumb consumer." |
| **Storage** | **Persistent Log**. Messages are stored on disk for a configurable period (e.g., days, weeks, or forever) and can be re-read. | **Message Queue**. Messages are typically removed once consumed and acknowledged. Primarily in-memory with disk backup. |
| **Throughput** | **Very High**. Optimized for sequential disk I/O and zero-copy, enabling millions of messages per second. | **Moderate to High**. Throughput can be limited by complex routing logic and message management overhead. |
| **Consumer Model** | **Consumer Groups**. Multiple consumers in a group share a topic, and each consumer gets a subset of partitions. Multiple groups can consume the same topic independently. | **Competing Consumers**. Multiple consumers on a single queue compete for messages. Once a message is consumed, it's gone. |
| **Best For** | High-volume event streaming, log aggregation, real-time analytics, event sourcing, data replication. | Traditional messaging, task queues, complex message routing, request/reply patterns. |

* **Best Practice:** Do not treat Kafka as a drop-in replacement for a traditional broker without understanding its pull-based nature and log-based storage. The application logic for consumers is different.


### Core Use Cases

* **Messaging:** Decoupling microservices. An `OrderService` can publish an `OrderCreated` event to a topic. An `InventoryService` and `NotificationService` can both consume this event to perform their respective tasks without being directly coupled.
* **Log Aggregation:** Collecting logs from many different servers and applications into central Kafka topics. This allows for standardized processing, monitoring, and analysis in tools like Elasticsearch or Splunk.
* **Event Sourcing:** Using Kafka as the primary source of truth. Instead of storing the current state of an application, you store the full sequence of events that led to the state. The state can be rebuilt at any time by replaying the events.
* **Stream Processing:** Performing real-time calculations, transformations, or aggregations on data streams. For example, a financial application could process a stream of stock trades to calculate a real-time moving average price.


### Core Concepts

* **Broker:** A single Kafka server. A cluster consists of multiple brokers working together. Each broker hosts a subset of partitions.
    * **Analogy:** A broker is like a single bookshelf in a massive library.
* **Topic:** A named stream of records. Topics are the primary unit of organization in Kafka.
    * **Analogy:** A topic is like a specific book title in the library (e.g., "The Adventures of Sherlock Holmes").
* **Partition:** A topic is divided into one or more partitions. Each partition is an ordered, immutable sequence of records that is continuously appended to. Partitions allow for parallelism, scalability, and fault tolerance.
    * **Analogy:** A partition is like a single volume or chapter of that book (e.g., "Volume 1," "Volume 2"). Each volume has its own ordered sequence of pages.
* **Offset:** A unique, sequential integer that identifies each record within a partition. Consumers track their position in each partition using offsets.
    * **Analogy:** An offset is like a page number within a specific book volume. It tells a reader exactly where they left off.

A simple command to create a topic:

```bash
# Creates a topic named 'orders' with 3 partitions and a replication factor of 1
kafka-topics.sh --bootstrap-server localhost:9092 --create --topic orders --partitions 3 --replication-factor 1
```

* **Common Pitfall:** A common mistake is to have too few partitions for a high-throughput topic, creating a bottleneck. The number of partitions determines the maximum level of consumer parallelism.

***
Would you like to continue with the next section, "Kafka Architecture"?

---

# yes

Of course. Here is the revision guide for Section 2: Kafka Architecture.

***

### 2. Kafka Architecture

Kafka's architecture is designed for high-throughput, scalability, and fault tolerance. It operates as a cluster of servers that work together to manage and store data streams.

#### Brokers and Clusters

* **Broker:** A single Kafka server. Each broker is identified by a unique integer ID.[^3_1]
* **Cluster:** A group of one or more brokers that work together. A cluster provides fault tolerance and load balancing. If one broker fails, the others can take over its work.[^3_2]

**Analogy:** A Kafka cluster is like a team of librarians (brokers) managing a large, distributed library. Each librarian is responsible for a specific set of book volumes (partitions).

#### ZooKeeper (legacy) vs. KRaft (Zookeeper-less mode)

Kafka has historically relied on Apache ZooKeeper for cluster coordination and metadata management. However, recent versions have introduced **KRaft** (Kafka Raft), which removes this dependency.[^3_3]


| Aspect | ZooKeeper-based Architecture | KRaft (Zookeeper-less) Architecture |
| :-- | :-- | :-- |
| **Metadata Storage** | Metadata (broker info, topic configs, ACLs) is stored in ZooKeeper [^3_4]. | Metadata is stored internally within Kafka in a special topic called `__cluster_metadata` [^3_4]. |
| **Coordination** | ZooKeeper manages controller election, tracks broker status, and stores configurations [^3_1]. | A quorum of dedicated `controller` nodes within the Kafka cluster manages metadata using the Raft consensus protocol [^3_3][^3_5]. |
| **Simplicity** | Requires a separate ZooKeeper ensemble, adding operational complexity (monitoring, security, tuning) [^3_6]. | Simplifies architecture by consolidating everything into Kafka. Fewer moving parts and easier to operate [^3_6]. |
| **Performance** | Can be a bottleneck for large clusters with frequent metadata changes. Slower recovery from controller failure [^3_3]. | Faster controller failover and metadata propagation. Scales to millions of partitions [^3_5]. |
| **Status** | Legacy. Still supported but being phased out. | **Production-ready** since Kafka 3.3. Will be the only mode in Kafka 4.0 [^3_3]. |

* **Kafka Version Note:** KRaft is the future of Kafka. New deployments should strongly consider using KRaft mode to reduce operational overhead.[^3_3]
* **Best Practice:** In KRaft, you can have dedicated controller nodes or have brokers serve both `broker` and `controller` roles. For large production clusters, separating the roles is recommended for better stability.[^3_7]


#### Leader Election and ISR (In-Sync Replicas)

For each partition, one broker is elected as the **leader**, and the other brokers hosting replicas become **followers**.[^3_1]

* **Leader:** Handles all read and write requests for that partition. There is only one leader per partition at any given time.
* **Followers:** Passively replicate data from the leader. They do not serve client requests but are ready to become the leader if the current one fails.[^3_1]
* **ISR (In-Sync Replicas):** This is the set of replicas that are fully caught-up with the leader's log. It always includes the leader itself.[^3_8]
    * A follower is removed from the ISR if it falls too far behind the leader (configurable via `replica.lag.time.max.ms`).[^3_9]
    * **Leader Election:** If a partition leader fails, a new leader is elected from the remaining brokers in the ISR. This ensures no data is lost, as any replica in the ISR is guaranteed to have the latest committed data.[^3_9]

**Analogy:** The partition leader is the "scribe" who is actively writing the story (data). The followers are "apprentices" copying the scribe's work in real-time. Only the apprentices who are perfectly up-to-date (in the ISR) are eligible to take over as the main scribe if the current one falls ill.

#### Controller Node

Within a Kafka cluster, one broker acts as the **active controller**. This broker has additional responsibilities for managing the cluster's state.[^3_10]

* **Responsibilities:**
    * Managing broker additions and removals.
    * Electing partition leaders and assigning followers.
    * Monitoring broker health.
* In a ZooKeeper cluster, the first broker to create an ephemeral node in ZooKeeper becomes the controller.[^3_10]
* In a KRaft cluster, the controller quorum elects an active controller among themselves.[^3_5]


#### High Watermark and Committed Offsets

* **High Watermark (HW):** This is the offset of the last message that has been successfully replicated to all replicas in the ISR. Consumers can only read messages up to the high watermark. This prevents consumers from reading data that has been written to the leader but not yet replicated, which could be lost if the leader fails. The HW is the offset of the latest available message + 1.[^3_11][^3_12]
* **Committed Offset:** This is a consumer-specific value. It's the offset of the last message a consumer has successfully processed, plus one. Consumers store (commit) this offset back to Kafka so they know where to resume reading after a restart or rebalance.[^3_11]

**Analogy:** The **High Watermark** is a "publication line" in our book analogy. A page (message) is only considered "published" and available to the public (consumers) once all the apprentice scribes (ISRs) have a confirmed copy. The **Committed Offset** is the personal bookmark of a reader, marking the last page they finished reading.

#### Request Processing Flow in Kafka

A simplified flow for produce and fetch requests:

1. **Request Arrival:** A client (producer or consumer) sends a request to a broker. The request lands in a socket receive buffer and is picked up by a **Network Thread**.[^3_13]
2. **Queuing:** The Network Thread places the request onto a shared **request queue**.[^3_13]
3. **I/O Processing:** An **I/O Thread** picks up the request.
    * **Produce Request:** The I/O thread validates the request and writes the data to the partition's log file (which is usually in the OS page cache). The request is then placed in "purgatory" until follower replicas have acknowledged the write.[^3_13]
    * **Fetch Request:** The I/O thread reads data from the log file. Kafka uses **zero-copy transfer** to efficiently send data from the page cache directly to the network socket, avoiding extra copies in user-space memory.[^3_13]
4. **Response:** Once the request is complete (e.g., acks received for a produce request), a response is generated and placed on a **response queue**, where a Network Thread sends it back to the client.[^3_13]

***
Would you like to continue with the next section, "Kafka Topics and Partitions"?
<span style="display:none">[^3_14][^3_15][^3_16][^3_17][^3_18][^3_19][^3_20]</span>

<div style="text-align: center">⁂</div>

[^3_1]: https://www.instaclustr.com/education/apache-kafka/apache-kafka-architecture-a-complete-guide-2025/

[^3_2]: https://www.geeksforgeeks.org/apache-kafka/kafka-architecture/

[^3_3]: https://www.openlogic.com/blog/kafka-raft-mode

[^3_4]: https://www.redpanda.com/guides/kafka-alternatives-kafka-raft

[^3_5]: https://docs.confluent.io/platform/current/kafka-metadata/kraft.html

[^3_6]: https://www.redpanda.com/guides/kafka-architecture-kafka-cluster

[^3_7]: https://www.digitalocean.com/community/tutorials/how-to-set-up-a-multi-node-kafka-cluster-using-kraft

[^3_8]: https://docs.confluent.io/kafka/design/replication.html

[^3_9]: https://www.geeksforgeeks.org/apache-kafka/understanding-in-sync-replicas-isr-in-apache-kafka/

[^3_10]: https://stackoverflow.com/questions/49525141/how-many-kafka-controllers-are-there-in-a-cluster-and-what-is-the-purpose-of-a-c

[^3_11]: https://www.reddit.com/r/apachekafka/comments/15uluwq/does_kafkas_high_watermark_offset_mean_the_offset/

[^3_12]: https://docs.confluent.io/platform/current/clients/confluent-kafka-dotnet/_site/api/Confluent.Kafka.WatermarkOffsets.html

[^3_13]: https://developer.confluent.io/courses/architecture/broker/

[^3_14]: https://kafka.apache.org/11/documentation/streams/architecture

[^3_15]: https://www.upsolver.com/blog/apache-kafka-architecture-what-you-need-to-know

[^3_16]: https://www.redpanda.com/guides/kafka-architecture

[^3_17]: https://developer.confluent.io/courses/architecture/get-started/

[^3_18]: https://kafka.apache.org/protocol

[^3_19]: https://www.interviewbit.com/blog/kafka-architecture/

[^3_20]: https://www.baeldung.com/kafka-shift-from-zookeeper-to-kraft


---

# yes

Certainly. Here is the revision guide for Section 3: Kafka Topics and Partitions.

***

### 3. Kafka Topics and Partitions

Topics and partitions are the fundamental units for organizing and scaling data in Kafka. Proper configuration is critical for performance and reliability.

#### Topic Creation \& Configuration

You can create topics using command-line tools or the AdminClient API. When creating a topic, you must specify the number of partitions and the replication factor.[^4_4]

```bash
# Create a topic 'user-signups' with 6 partitions and a replication factor of 3
kafka-topics.sh --bootstrap-server broker1:9092 --create \
  --topic user-signups \
  --partitions 6 \
  --replication-factor 3 \
  --config "min.insync.replicas=2" \
  --config "retention.ms=604800000" # 7 days
```

* **Best Practice:** Always explicitly set key configurations like `retention.ms` and `min.insync.replicas` during topic creation rather than relying on broker defaults. This makes your topic's behavior predictable and self-contained.[^4_5]


#### Partition Count and Replication Factor

* **Partition Count:** Determines the level of parallelism. A topic with 10 partitions can be consumed by at most 10 consumers within the same consumer group.[^4_2]
    * **Analogy:** If a checkout counter is a topic, partitions are the individual checkout lanes. More lanes allow more customers (consumers) to be served simultaneously.
    * **Best Practice:** Choose a partition count based on your target throughput and the number of consumer instances you plan to run. It's easy to add more partitions later, but you cannot decrease the count. Adding partitions can break key-based ordering guarantees if not handled carefully.[^4_5]
* **Replication Factor:** The number of copies of each partition that exist in the cluster. A replication factor of `N` allows for `N-1` broker failures without data loss. A typical value for production is 3.[^4_5]


#### Log Segmentation and Retention

Each partition is an append-only log, but on disk, it's broken into smaller files called **log segments**.

* When a segment reaches a certain size (e.g., 1GB, set by `segment.bytes`) or age (`segment.ms`), it is closed, and a new active segment is created.
* Retention policies operate on these closed segments.


#### Cleanup Policies: `delete` vs. `compact`

The `cleanup.policy` configuration determines what happens to old data.


| Policy | Behavior | Use Case |
| :-- | :-- | :-- |
| **`delete` (default)** | Old log segments are deleted either when their retention time (`retention.ms`) or size (`retention.bytes`) is exceeded. | General-purpose data streaming where historical data becomes irrelevant after a certain period (e.g., metrics, application logs). |
| **`compact`** | Guarantees to keep at least the *last known value for each message key* within a partition. Older records with the same key are removed. `null` values are treated as "tombstones" and cause the key to be deleted entirely. | Storing the current state of objects, like user profiles or database change data capture (CDC) events. Useful for KTables in Kafka Streams. |
| **`delete,compact`** | You can use both. Compaction ensures the latest value for each key is retained, while the delete policy can still remove very old data, including the latest value, if it exceeds the retention time. | A common pattern is to compact data but also enforce an absolute maximum retention period for compliance or storage reasons. |

* **Log Compaction Internals:** A background process called the Log Cleaner thread periodically runs on brokers. It scans log segments and rewrites them, removing records that are "shadowed" by newer records with the same key. This process only runs on the "clean" (inactive) portion of the log.


#### `min.insync.replicas` (min.isr)

This is a critical configuration for data durability. It specifies the minimum number of replicas that must be in the ISR (including the leader) for a producer to successfully write a message when using `acks=all` (or `-1`).

* **Example:** If `replication.factor=3` and `min.insync.replicas=2`, a produce request will succeed only if the leader and at least one follower acknowledge the write. The cluster can tolerate one broker failure without losing write availability.
* **Common Pitfall:** Setting `min.insync.replicas` equal to `replication.factor` (e.g., both 3) maximizes durability but sacrifices availability. If just one replica goes down or becomes slow, producers will fail. A common best practice is to set `min.insync.replicas` to `replication.factor - 1`.

***
Would you like to continue with the next section, "Kafka Producers"?
<span style="display:none">[^4_1][^4_3][^4_6][^4_7][^4_8]</span>

<div style="text-align: center">⁂</div>

[^4_1]: https://stackoverflow.com/questions/38024514/understanding-kafka-topics-and-partitions

[^4_2]: https://developer.confluent.io/courses/apache-kafka/partitions/

[^4_3]: https://www.baeldung.com/kafka-topics-partitions

[^4_4]: https://www.geeksforgeeks.org/java/topics-partitions-and-offsets-in-apache-kafka/

[^4_5]: https://newrelic.com/blog/best-practices/effective-strategies-kafka-topic-partitioning

[^4_6]: https://www.instaclustr.com/education/apache-kafka/apache-kafka-architecture-a-complete-guide-2025/

[^4_7]: https://www.youtube.com/watch?v=tipFUfxEIYg

[^4_8]: https://dev.to/jhonifaber/understanding-apache-kafka-topics-partitions-brokers-2182


---

# yes

Absolutely. Here is the revision guide for Section 4: Kafka Producers.

***

### 4. Kafka Producers

A producer is a client application that writes streams of records to Kafka topics. The producer is responsible for serialization, partitioning, compression, and handling acknowledgements from the brokers.[^5_1]

#### Kafka Producer API

A producer is created with a set of properties, and then used to send `ProducerRecord` objects.

**Real-World Example (Java):**

```java
// 1. Configure producer properties
Properties props = new Properties();
props.put("bootstrap.servers", "localhost:9092");
props.put("key.serializer", "org.apache.kafka.common.serialization.StringSerializer");
props.put("value.serializer", "org.apache.kafka.common.serialization.StringSerializer");

// 2. Create the producer
Producer<String, String> producer = new KafkaProducer<>(props);

// 3. Create a record to send
ProducerRecord<String, String> record = 
    new ProducerRecord<>("order-topic", "user-123", "order-details-json");

// 4. Send the record (asynchronously by default)
producer.send(record, (metadata, exception) -> {
    if (exception == null) {
        System.out.printf("Sent record to partition %d at offset %d%n",
            metadata.partition(), metadata.offset());
    } else {
        exception.printStackTrace();
    }
});

// 5. Close the producer to ensure all buffered records are sent
producer.close();
```


#### Keyed vs. Keyless Records

* **Keyed Records:** When a record has a key, Kafka guarantees that all records with the same key will always be sent to the same partition. This is essential for ensuring ordering for a specific entity (e.g., all events for a single user ID).[^5_1]
* **Keyless Records (`key=null`):** When no key is provided, records are distributed across partitions in a round-robin fashion to balance the load.
    * **Kafka Version Note:** Prior to Kafka 2.4, the default was simple round-robin. Since 2.4, the default behavior uses "sticky partitioning." The producer "sticks" to one partition for a short time to create larger batches, reducing latency and broker load. It only switches partitions when a batch is full or `linger.ms` is met.


#### Partitioning Strategies

The producer uses a partitioner to determine which partition to send a record to:

1. **Explicit Partition:** If a partition number is specified in the `ProducerRecord`, that partition is used.
2. **Key-Based:** If no partition is specified but a key is present, the key is hashed to select a partition. The default partitioner uses a `murmur2` hash of the key.
3. **Round-Robin/Sticky:** If neither a partition nor a key is present, the sticky partitioning strategy is used.
4. **Custom Partitioner:** You can implement your own `Partitioner` interface for custom logic (e.g., sending high-priority customers to specific partitions).

#### Acknowledgement Modes (`acks`)

This setting controls the durability guarantees for produced messages.


| `acks` Setting | Description | Pro | Con |
| :-- | :-- | :-- | :-- |
| **`acks=0`** (Fire and Forget) | The producer does not wait for any acknowledgement from the broker. | Highest throughput, lowest latency. | High risk of message loss. No retries. |
| **`acks=1`** (Leader Ack) | The producer waits for an acknowledgement from the partition leader only. | Good balance of durability and performance. | Message loss can occur if the leader fails before followers replicate the data. |
| **`acks=all` (or `-1`)** | The producer waits for acknowledgement from the leader *and* all in-sync replicas (ISRs). | Strongest durability guarantee. No message loss if at least one ISR remains. | Highest latency. Requires `min.insync.replicas` to be configured correctly. |

* **Best Practice:** For critical data, always use **`acks=all`** combined with a `min.insync.replicas` setting of 2 or more.


#### Batching and Compression

* **Batching:** To improve efficiency, producers automatically collect records destined for the same partition into batches before sending them.
    * `batch.size`: The maximum size in bytes of a batch.
    * `linger.ms`: The maximum time a producer will wait to fill a batch before sending it.
* **Compression:** Producers can compress batches of messages, which reduces network bandwidth and storage requirements.
    * `compression.type`: Can be set to `snappy`, `gzip`, `lz4`, or `zstd`.
    * **Best Practice:** **`Snappy`** and **`LZ4`** offer a good balance of compression ratio and low CPU overhead. **`ZSTD`**, introduced in Kafka 2.1, often provides the best compression ratio with performance comparable to LZ4.


#### Idempotent Producers \& Exactly-Once Semantics (EOS)

* **Idempotent Producer (`enable.idempotence=true`):** Prevents duplicate messages from being written in the event of producer retries. Each producer is assigned a unique ID (PID), and each message is given a sequence number. The broker tracks the latest sequence number for each PID and discards any duplicates.
    * **Best Practice:** Enabling idempotence is highly recommended as it has minimal performance overhead. When `enable.idempotence` is `true`, `acks` automatically defaults to `all` and `retries` defaults to a large value.
* **Transactions (EOS):** For "exactly-once" processing across multiple partitions/topics (e.g., read-process-write patterns), you can use the transactional API. This ensures that a group of messages is either successfully written to all target partitions or none at all (atomic writes). This is achieved by setting a `transactional.id` in the producer config.

***
Would you like to continue with the next section, "Kafka Consumers"?
<span style="display:none">[^5_2][^5_3][^5_4][^5_5][^5_6][^5_7][^5_8]</span>

<div style="text-align: center">⁂</div>

[^5_1]: https://www.instaclustr.com/education/apache-kafka/apache-kafka-architecture-a-complete-guide-2025/

[^5_2]: https://www.geeksforgeeks.org/apache-kafka/kafka-architecture/

[^5_3]: https://developer.confluent.io/courses/architecture/get-started/

[^5_4]: https://kafka.apache.org/11/documentation/streams/architecture

[^5_5]: https://www.tutorialspoint.com/apache_kafka/apache_kafka_fundamentals.htm

[^5_6]: https://www.anuragkapur.com/assets/blog/engineering/apache-kafka/slidesapachekafkaarchitecturefundamentalsexplained1579807020653.pdf

[^5_7]: https://www.slideshare.net/slideshow/apache-kafka-architectures-and-fundamentals/238841339

[^5_8]: https://www.youtube.com/watch?v=QkdkLdMBuL0


---

# yes

Of course. Here is the revision guide for Section 5: Kafka Consumers.

***

### 5. Kafka Consumers

A consumer is a client application that reads and processes streams of records from Kafka topics. Consumers operate in groups and are designed to be scalable and fault-tolerant.[^6_5]

#### Kafka Consumer API

Consumers subscribe to topics and poll for data in a loop.

**Real-World Example (Java):**

```java
// 1. Configure consumer properties
Properties props = new Properties();
props.put("bootstrap.servers", "localhost:9092");
props.put("group.id", "payment-processing-group"); // Essential for consumer groups
props.put("key.deserializer", "org.apache.kafka.common.serialization.StringDeserializer");
props.put("value.deserializer", "org.apache.kafka.common.serialization.StringDeserializer");
props.put("auto.offset.reset", "earliest"); // Start reading from the beginning if no offset is found
props.put("enable.auto.commit", "false"); // We will commit offsets manually

// 2. Create the consumer
Consumer<String, String> consumer = new KafkaConsumer<>(props);

// 3. Subscribe to one or more topics
consumer.subscribe(Arrays.asList("order-topic"));

// 4. Start the polling loop
while (true) {
    ConsumerRecords<String, String> records = consumer.poll(Duration.ofMillis(100));
    for (ConsumerRecord<String, String> record : records) {
        System.out.printf("Processing record from partition %d with offset %d%n",
            record.partition(), record.offset());
        // Process the record here...
    }
    // 5. Commit offsets manually after processing a batch
    consumer.commitSync(); 
}
// consumer.close(); // Should be in a finally block
```


#### Consumer Groups

A **consumer group** is a set of consumers that cooperate to consume data from a topic. Each consumer in the group is assigned a unique set of partitions from the topic. This is how Kafka achieves scalable consumption.[^6_4]

* If you have a topic with 10 partitions and a consumer group with 10 consumers, each consumer will read from exactly one partition.
* If you add more consumers to the group (e.g., 12 consumers), 2 of them will remain idle.
* If a consumer leaves the group (crashes or shuts down), its partitions are automatically reassigned to the remaining consumers. This process is called a **rebalance**.

**Analogy:** A consumer group is a team of workers assigned to unload cargo containers (partitions). Each worker is assigned their own set of containers. If a worker goes on break, their containers are distributed among the other team members to keep the work going.

#### The Polling Model

Consumers **pull** data from Kafka. The `consumer.poll()` method is the heart of the consumer client. It fetches data, manages heartbeats to keep the session alive, and triggers rebalances.

* `max.poll.records`: The maximum number of records returned in a single call to `poll()`.
* `max.poll.interval.ms`: The maximum time allowed between calls to `poll()`. If a consumer fails to call `poll()` within this interval, it is considered dead, and its partitions will be reassigned.
* **Common Pitfall:** Performing long-running processing within the poll loop can exceed `max.poll.interval.ms`, causing constant rebalances. Process heavy tasks in a separate thread pool.


#### Rebalancing Strategies

When consumers join or leave a group, a rebalance occurs to redistribute partitions.

* **`Range` \& `RoundRobin`:** Legacy "stop-the-world" strategies. All consumers stop processing, give up their partitions, and wait for a new assignment. This can cause a short service interruption.
* **`Sticky`:** An improvement over Range/RoundRobin. Tries to keep existing partition assignments as "sticky" as possible during a rebalance, minimizing partition movement.
* **`CooperativeSticky` (Incremental Rebalancing):** The current default. Rebalances happen in two stages. Consumers can continue processing partitions that are not affected by the rebalance, resulting in much less disruption.


#### Offset Management

The consumer needs to track which messages it has already processed. This position is called the offset.

* **Auto Commit (`enable.auto.commit=true`):** The consumer automatically commits offsets in the background at a configured interval (`auto.commit.interval.ms`). This is convenient but can lead to missed or duplicate messages if a failure occurs after a commit but before processing is complete.
* **Manual Commit:** Gives the developer full control.
    * `commitSync()`: Commits the last offsets returned by `poll()` and blocks until the commit succeeds or fails. It will retry on failure.
    * `commitAsync()`: Sends the commit request and continues without blocking. Faster, but does not retry on failure.
* **Best Practice:** Use **manual commit** for most applications to ensure at-least-once or exactly-once processing. Commit offsets only after you are sure the records have been fully processed.


#### Error Handling

* **Deserialization Errors:** By default, a deserialization error will cause the consumer to fail. You can configure it to skip the problematic message and continue.
* **Processing Failures:** If your application fails to process a record, you can implement retry logic.
* **Dead Letter Topics (DLT):** A common pattern is to catch processing exceptions, send the failing message to a separate "dead-letter" topic for later analysis, and then commit the offset for the original message to move on.

***
Would you like to continue with the next section, "Kafka Delivery Semantics"?
<span style="display:none">[^6_1][^6_2][^6_3][^6_6][^6_7][^6_8][^6_9]</span>

<div style="text-align: center">⁂</div>

[^6_1]: https://learn.conduktor.io/kafka/complete-kafka-consumer-with-java/

[^6_2]: https://kafka.apache.org/31/javadoc/org/apache/kafka/clients/consumer/KafkaConsumer.html

[^6_3]: https://www.baeldung.com/java-kafka-consumer-api-read

[^6_4]: https://docs.confluent.io/kafka-clients/java/current/overview.html

[^6_5]: https://www.svix.com/guides/kafka/java-kafka-consumer/

[^6_6]: https://www.sohamkamani.com/java/kafka/

[^6_7]: https://www.geeksforgeeks.org/apache-kafka/apache-kafka-create-consumer-using-java/

[^6_8]: https://learn.microsoft.com/en-us/azure/hdinsight/kafka/apache-kafka-producer-consumer-api

[^6_9]: https://kafka.apache.org/documentation/


---

# yes

Absolutely. Here is the revision guide for Section 6: Kafka Delivery Semantics.

***

### 6. Kafka Delivery Semantics

Delivery semantics define the guarantees a system provides for message delivery between a producer and a consumer. Kafka can be configured to support different levels of guarantees, each with its own trade-offs.

#### At-most-once

* **Guarantee:** Messages are delivered zero or one time. Messages might be lost, but they are never redelivered.
* **How it works (Producer):** Producer sets `acks=0`. It sends the message and doesn't wait for a broker acknowledgement. If the broker is down or the network fails, the message is lost.
* **How it works (Consumer):** Consumer commits offsets *before* processing the messages. If the consumer crashes after committing but before processing, the messages are lost forever upon restart.
* **Use Case:** Non-critical data where occasional loss is acceptable, such as collecting metrics or logging. Prioritizes performance over reliability.


#### At-least-once

* **Guarantee:** Messages are never lost, but they might be delivered more than once.
* **How it works (Producer):** Producer sets `acks=1` or `acks=all`. If the producer doesn't receive an acknowledgement (e.g., due to a temporary network issue), it will retry sending the message. This can lead to the broker writing the same message multiple times.
* **How it works (Consumer):** Consumer commits offsets *after* processing the messages. If the consumer crashes after processing but before committing, it will re-process the same messages upon restart, leading to duplicates.
* **Use Case:** The most common semantic. Suitable for many applications like e-commerce order processing or analytics pipelines, where the downstream system can handle duplicates (e.g., through idempotent operations).


#### Exactly-once Semantics (EOS)

* **Guarantee:** Each message is delivered once and only once, even in the presence of failures.
* **How it works:** EOS is achieved by combining two key features:

1. **Idempotent Producer:** `enable.idempotence=true`. This prevents duplicates from producer-side retries. The broker keeps track of the producer's message sequence numbers and discards any duplicates.
2. **Transactions:** For consumer applications that read from a topic and then write to another (a "read-process-write" pattern), transactions are used to link the consumer offset commits and the producer's writes into a single atomic operation.


#### Transactions and Atomic Writes

The Kafka transactional API allows a producer to send a batch of messages to multiple partitions and topics atomically.

**Real-World Example (Simplified Flow for EOS):**

1. A producer is configured with `transactional.id` and `enable.idempotence=true`.
2. The producer calls `beginTransaction()`.
3. A consumer application fetches records from an input topic (e.g., `topic-A`).
4. The application processes these records.
5. The producer sends the results to an output topic (e.g., `topic-B`) within the same transaction.
6. The producer then sends the consumer's offsets to commit to a special internal topic, also within the transaction.
7. The producer calls `commitTransaction()`.

If any step fails, the producer calls `abortTransaction()`, and none of the changes (produced messages or committed offsets) become visible to other consumers.

**Comparison Table**


| Semantic | Producer Config | Consumer Logic | Performance | Complexity |
| :-- | :-- | :-- | :-- | :-- |
| **At-most-once** | `acks=0` | Commit before processing. | Highest | Lowest |
| **At-least-once** | `acks=all` | Commit after processing. | High | Low |
| **Exactly-once** | `enable.idempotence=true`, `transactional.id` | Use transactional API to link commits and writes. | Lower (due to coordination) | Highest |

* **Common Pitfall:** EOS in Kafka only guarantees exactly-once delivery *within the Kafka ecosystem*. If your consumer's processing involves writing to an external system like a database, you must use a two-phase commit protocol or ensure the external system write is idempotent to achieve true end-to-end exactly-once processing.

***
Would you like to continue with the next section, "Kafka Configuration \& Tuning"?
<span style="display:none">[^7_1][^7_2][^7_3][^7_4][^7_5][^7_6][^7_7][^7_8][^7_9]</span>

<div style="text-align: center">⁂</div>

[^7_1]: https://www.instaclustr.com/blog/kafka-streams-guide/

[^7_2]: https://kafka.apache.org/documentation/streams/

[^7_3]: https://docs.confluent.io/platform/current/streams/concepts.html

[^7_4]: https://www.baeldung.com/java-kafka-streams

[^7_5]: https://developer.confluent.io/courses/kafka-streams/get-started/

[^7_6]: https://www.youtube.com/watch?v=y9a3fldlvnI

[^7_7]: https://www.geeksforgeeks.org/java/apache-kafka-streams-simple-word-count-example/

[^7_8]: https://www.reddit.com/r/apachekafka/comments/qmpvjk/learning_kafka_streams/

[^7_9]: https://www.youtube.com/watch?v=MR5hllNC9hk


---

# yes

Excellent. Here is the revision guide for Section 7: Kafka Configuration \& Tuning.

***

### 7. Kafka Configuration \& Tuning

Proper configuration is key to optimizing Kafka for performance, latency, and throughput. Tuning involves adjusting parameters at the broker, producer, consumer, and topic levels. It's crucial to avoid using default settings for production workloads, as they are often not optimized for performance or cost-efficiency.[^8_5]

#### Broker Configs (`server.properties`)

These are the most critical settings for the Kafka brokers themselves.


| Property | Description \& Recommendation |
| :-- | :-- |
| **`num.partitions`** | Default number of partitions for auto-created topics. **Best Practice:** Disable topic auto-creation (`auto.create.topics.enable=false`) in production and define partitions explicitly per topic [^8_5]. |
| **`log.retention.{hours|ms|bytes}`** | Controls default data retention. Set a sensible default, but override it at the topic level based on use case [^8_1]. |
| **`log.segment.bytes`** | The size of a single log file segment on disk (default is 1GB). Smaller segments can lead to faster cleanup and recovery but more file handles [^8_5]. |
| **`min.insync.replicas`** | Default minimum number of in-sync replicas for writes with `acks=all`. Setting this at the broker level provides a safety net. |
| **`num.network.threads`** / **`num.io.threads`** | The number of threads used for network and disk I/O. Default is often fine, but for high-load clusters, increasing these (e.g., to match the number of CPU cores) can help. |

#### Producer and Consumer Tuning Parameters

Tuning clients can drastically impact performance without changing the broker setup.[^8_5]

**Producer Tuning for Throughput:**

* **`batch.size`**: Controls the maximum size of a message batch. Larger batches (e.g., 64-128KB) improve throughput by reducing the number of requests.[^8_7]
* **`linger.ms`**: The delay before sending a batch, allowing it to fill up. A value of 5-25ms is a good starting point to increase batching without adding significant latency.[^8_7]
* **`compression.type`**: Use `lz4` or `zstd` to reduce network I/O and storage needs at the cost of some CPU.[^8_7]
* **`buffer.memory`**: Total memory available to the producer for buffering records. Must be large enough to handle `batch.size` for all in-flight batches.[^8_7]

**Consumer Tuning for Latency vs. Throughput:**

* **`fetch.min.bytes`**: The minimum amount of data the consumer will fetch from the broker. A larger value reduces broker load but increases latency, as the consumer waits for more data.[^8_5]
* **`fetch.max.wait.ms`**: The maximum time the broker will wait for `fetch.min.bytes` to be met. This pair of settings allows you to balance latency and throughput.[^8_5]
* **`max.poll.records`**: Maximum number of records returned in a single `poll()` call. A smaller number means faster processing loops but more requests. Adjust based on how long it takes to process a single record.[^8_5]
* **`session.timeout.ms`** / **`heartbeat.interval.ms`**: Controls consumer failure detection. A common practice is to set `heartbeat.interval.ms` to one-third of `session.timeout.ms`.[^8_6]


#### Topic-level Configurations

You can override broker-level defaults for each topic, which is a powerful way to tailor behavior.

```bash
# Example: Altering a topic to use compaction and a shorter retention
kafka-configs.sh --bootstrap-server localhost:9092 --alter --topic my-topic \
  --add-config cleanup.policy=compact,retention.ms=86400000
```

* **Best Practice:** Always manage configurations on a per-topic basis for production systems. This prevents a global change from negatively impacting an unrelated application.[^8_1]


#### Tuning for Performance, Latency, and Throughput

This is always a game of trade-offs.


| To Optimize For... | Key Parameters to Adjust | Trade-off |
| :-- | :-- | :-- |
| **High Throughput** | Increase producer `batch.size` \& `linger.ms`. Use efficient `compression.type`. Increase `num.partitions`. | Increases end-to-end latency. |
| **Low Latency** | Decrease producer `linger.ms` to 0. Decrease consumer `fetch.min.bytes` and `fetch.max.wait.ms`. | Decreases throughput (more, smaller requests). Increases CPU load on brokers. |
| **High Durability** | Producer: `acks=all`. Topic: `replication.factor=3`, `min.insync.replicas=2`. | Increases producer latency. Reduces availability if ISR count drops below `min.insync.replicas`. |

#### OS, JVM, and Disk Tuning for Kafka

* **OS Tuning:** Kafka heavily relies on the OS page cache. Ensure you have ample RAM. Use XFS or ext4 filesystems. Increase the file descriptor limit (`ulimit -n`).
* **JVM Tuning:** Dedicate a significant portion of heap space to Kafka (e.g., 6-8 GB is common), but leave plenty of memory for the page cache. The OS will use all remaining free RAM for this. Use the G1 garbage collector for better pause-time behavior.
* **Disk:** Use fast disks (SSDs are ideal) for broker log directories. If using HDDs, use multiple disks and configure `log.dirs` with a comma-separated list of paths to spread the I/O load.

***
Would you like to continue with the next section, "Kafka Internals"?
<span style="display:none">[^8_2][^8_3][^8_4][^8_8][^8_9]</span>

<div style="text-align: center">⁂</div>

[^8_1]: https://www.instaclustr.com/education/apache-kafka/12-kafka-best-practices-run-kafka-like-the-pros/

[^8_2]: https://docs.confluent.io/platform/current/kafka/post-deployment.html

[^8_3]: https://newrelic.com/blog/best-practices/kafka-best-practices

[^8_4]: https://www.groundcover.com/blog/kafka-consumer-best-practices

[^8_5]: https://stackoverflow.blog/2024/09/04/best-practices-for-cost-efficient-kafka-clusters/

[^8_6]: https://learn.microsoft.com/en-us/azure/event-hubs/apache-kafka-configurations

[^8_7]: https://docs.aws.amazon.com/msk/latest/developerguide/bestpractices-kafka-client.html

[^8_8]: https://www.redpanda.com/guides/kafka-performance-kafka-optimization

[^8_9]: https://kafka.apache.org/documentation/


---

# yes

Of course. Here is the revision guide for Section 8: Kafka Internals.

***

### 8. Kafka Internals

Understanding Kafka's internal mechanics reveals why it is so fast and resilient. It's a system deeply optimized for disk and network I/O.

#### Storage Structure and Log Segments

A partition is not a single, massive file. Instead, it is a directory of **log segment files**.

* Each partition directory contains `.log` files (the data), `.index` files (offset-to-position mapping), and `.timeindex` files (timestamp-to-offset mapping).
* Only one segment is the **active segment**; it's the only file that is ever written to.
* When the active segment reaches a certain size (`segment.bytes`) or age (`segment.ms`), it is "rolled," becoming a read-only, inactive segment. A new active segment is then created.
* This segmentation strategy makes cleanup policies (deletion and compaction) easy to implement, as they only need to operate on whole, inactive segments.

**Analogy:** A partition is like a multi-volume journal. The author only ever writes in the newest volume (the active segment). Once a volume is full, it's put on the shelf with the others (inactive segments) and can be read, archived, or eventually discarded.

#### Indexes and File Compaction

* **Indexes:** For each `.log` segment, there's a corresponding `.index` file. This index maps a message's logical offset to its physical byte position within the `.log` file. This allows Kafka to quickly locate any message by its offset without scanning the entire log file.
* **File Compaction (`cleanup.policy=compact`):** The **Log Cleaner** is a pool of background threads on the broker.

1. It scans the "dirty" (inactive) segments of a compacted topic.
2. It builds an in-memory map of the last known value for each key.
3. It then rewrites the log segment, keeping only the records corresponding to the latest keys.
4. The old, "dirty" segment is swapped with the new, "clean" one.


#### Page Cache and Zero-Copy Transfer

Kafka's performance relies heavily on the operating system's **page cache**.

* When a producer writes to a broker, the data is written to the OS page cache first, which is extremely fast. The OS then handles flushing this data to the physical disk in the background.
* When a consumer reads data, it is often served directly from this same page cache, avoiding slow disk reads.
* **Zero-Copy Transfer:** Kafka uses a kernel-level optimization called `sendfile()`. When a consumer requests data that is in the page cache, the OS can send the data directly from the page cache to the network socket without ever copying it into the Kafka application's memory (user space). This avoids redundant data copies and CPU cycles, making data transfer extremely efficient.


#### Flush Policies and `fsync` behavior

* Kafka does not immediately force writes to disk (`fsync`). It trusts the OS to handle flushing from the page cache. This is a key reason for its high throughput.
* Reliability is not compromised because of the replication mechanism. If a leader broker crashes before data is flushed to its disk, a fully synced follower (which also has the data in its page cache) will take over.
* You can configure flush policies (`log.flush.interval.ms`, `log.flush.interval.messages`), but this is generally discouraged as it severely impacts performance and offers little benefit in a replicated setup.


#### Leader/Follower Synchronization and ISR Behavior

* **Synchronization:** Followers constantly send Fetch requests to their partition leader. The leader returns new messages, and the follower appends them to its own log.
* **ISR Shrink/Expand Behavior:**
    * **Shrink:** A follower is removed from the ISR if it falls behind the leader's log end offset for a time exceeding `replica.lag.time.max.ms` (default 30s). This can happen if the follower is slow, has network issues, or is restarting.
    * **Expand:** A follower that was previously out of sync can rejoin the ISR once it has fully caught up to the leader's log.

***
Would you like to continue with the next section, "Kafka Streams API"?
<span style="display:none">[^9_1][^9_2][^9_3][^9_4][^9_5][^9_6][^9_7][^9_8]</span>

<div style="text-align: center">⁂</div>

[^9_1]: https://www.redpanda.com/guides/kafka-cloud-kafka-authentication

[^9_2]: https://developer.confluent.io/courses/security/authentication-basics/

[^9_3]: https://developer.ibm.com/tutorials/kafka-authn-authz/

[^9_4]: https://www.scaler.com/topics/kafka-tutorial/kafka-authentication/

[^9_5]: https://www.tencentcloud.com/techpedia/107870

[^9_6]: https://www.baeldung.com/ops/kafka-authentication-topics-sh

[^9_7]: https://docs.aws.amazon.com/msk/latest/developerguide/kafka_apis_iam.html

[^9_8]: https://kafka.apache.org/090/documentation.html


---

# yes

Certainly. Here is the revision guide for Section 9: Kafka Streams API.

***

### 9. Kafka Streams API

Kafka Streams is a client library for building real-time streaming applications and microservices where the input and output data are stored in Kafka topics. It is not a separate cluster but a Java library that you embed in your own application.[^10_1][^10_2]

#### KStream, KTable, and GlobalKTable

These are the core abstractions in the Streams DSL (Domain-Specific Language).


| Abstraction | Description | Analogy |
| :-- | :-- | :-- |
| **KStream** | An unbounded stream of key-value records. Each new record is an independent piece of data, like an entry in a log. | A stream of news headlines. Each headline is a new, distinct event. |
| **KTable** | A view of a stream as a changelog. It represents the latest value for each key. When a new record with an existing key arrives, it's an *update*. | A table of current stock prices. Each new record for "AAPL" updates the current price of Apple stock. |
| **GlobalKTable** | A KTable where the *entire* table's data is replicated to every instance of your application. | A small lookup table, like a mapping of country codes to country names. Every application instance has the full list locally. |

#### Stateless vs. Stateful Processing

* **Stateless Operations:** These operations don't require knowledge of past events. They process each record independently.
    * **Examples:** `map`, `flatMap`, `filter`, `branch`.
    * `filter`: Keep only records that match a predicate.
    * `map`: Transform a record into a new record (e.g., change its value or key).
* **Stateful Operations:** These operations require maintaining a state over time, derived from the records that have been processed.
    * **Examples:** `count`, `reduce`, `aggregate`.
    * `count`: Count the number of records by key.
    * `aggregate`: A more general form of `count` and `reduce` where you can define how to add records to and remove records from an aggregation.


#### Joins

Kafka Streams allows you to join different streams and tables.


| Join Type | Description | Use Case |
| :-- | :-- | :-- |
| **KStream-KStream** | Joins records from two streams that occur within a specified time window. | Joining a stream of ad clicks with a stream of ad impressions to see which impressions led to clicks. |
| **KStream-KTable** | Enriches a stream of events with data from a table. This is a very common pattern. | Enriching a stream of `Order` events (KStream) with `Customer` details (KTable) based on the `customerId`. |
| **KTable-KTable** | Joins two KTables, creating a new KTable that is updated whenever either of the source tables is updated. | Joining a table of user profiles with a table of user preferences. |

#### Windowed Aggregations

Stateful operations can be performed over a "window" of time.

* **Tumbling Window:** Fixed-size, non-overlapping windows. E.g., counting events every 5 minutes.
* **Hopping Window:** Fixed-size, overlapping windows. E.g., a 5-minute window that "hops" forward every 1 minute.
* **Sliding Window:** A window that is defined dynamically around each record, including records that arrive a fixed time before or after it.
* **Session Window:** Groups records for a key that occur within a certain period of "inactivity." Useful for tracking user sessions.


#### Fault Tolerance and State Stores

* Stateful operations require a **state store** to hold the current aggregation, join state, etc.
* By default, Kafka Streams uses **RocksDB**, an embedded key-value store, for local state on each application instance.
* For fault tolerance, the state store is backed up by a **changelog topic** in Kafka. If an application instance fails, a new instance can restore its state by replaying the changelog topic.


#### DSL vs. Processor API

* **DSL (Domain-Specific Language):** A high-level, fluent API that covers most common use cases (`map`, `filter`, `join`, `groupBy`, etc.). It's declarative and easy to use.
* **Processor API:** A lower-level, imperative API that gives you fine-grained control. You can define custom processors, interact directly with state stores, and schedule periodic functions (punctuations).
* **Best Practice:** Start with the DSL. Drop down to the Processor API only when the DSL doesn't meet your specific needs. You can also mix both in a single topology.

**Real-World Example (Java DSL - Word Count):**

```java
StreamsBuilder builder = new StreamsBuilder();

// 1. Create a KStream from the input topic
KStream<String, String> textLines = builder.stream("lines-of-text-topic");

// 2. Split lines into words (flatMap), group by word (groupBy), and count (count)
KTable<String, Long> wordCounts = textLines
    .flatMapValues(value -> Arrays.asList(value.toLowerCase().split("\\W+")))
    .groupBy((key, word) -> word)
    .count(Materialized.as("counts-store")); // The result is a KTable

// 3. Write the KTable's changelog stream to an output topic
wordCounts.toStream().to("word-counts-topic", Produced.with(Serdes.String(), Serdes.Long()));

// Build and start the topology
KafkaStreams streams = new KafkaStreams(builder.build(), props);
streams.start();
```


***
Would you like to continue with the next section, "Kafka Connect"?
<span style="display:none">[^10_3][^10_4][^10_5][^10_6][^10_7][^10_8][^10_9]</span>

<div style="text-align: center">⁂</div>

[^10_1]: https://developer.confluent.io/courses/kafka-streams/get-started/

[^10_2]: https://kafka.apache.org/documentation/streams/

[^10_3]: https://www.instaclustr.com/blog/kafka-streams-guide/

[^10_4]: https://www.baeldung.com/java-kafka-streams

[^10_5]: https://www.instaclustr.com/support/documentation/kafka/using-kafka/working-with-kafka-streams-api/

[^10_6]: https://www.youtube.com/watch?v=FOLh1LuEw7c

[^10_7]: https://learn.microsoft.com/en-us/azure/hdinsight/kafka/apache-kafka-streams-api

[^10_8]: https://docs.confluent.io/platform/current/streams/concepts.html

[^10_9]: https://developer.ibm.com/tutorials/developing-a-streams-processor-with-apache-kafka/


---

# yes

Excellent. Here is the revision guide for Section 10: Kafka Connect.

***

### 10. Kafka Connect

Kafka Connect is a framework for scalably and reliably streaming data between Apache Kafka and other systems. It's a tool that runs as a separate service from your Kafka brokers and provides a pluggable architecture for moving data with no custom code required for common data sources and sinks.[^11_4][^11_5][^11_6]

#### Introduction to Kafka Connect

The core idea of Kafka Connect is to provide a standardized way to create **connectors**, which are ready-to-use components for pulling data into Kafka or pushing data out of Kafka. This eliminates the need for every developer to write a custom producer or consumer for each external system they want to integrate with.[^11_2]

#### Source and Sink Connectors

There are two types of connectors :[^11_2]

* **Source Connectors:** Ingest data from external systems (sources) and write it into Kafka topics.
    * **Real-World Example:** A **JDBC Source Connector** can monitor a database table for new or updated rows and write each change as a message to a Kafka topic.
* **Sink Connectors:** Read data from Kafka topics and write it to external systems (sinks).
    * **Real-World Example:** An **Elasticsearch Sink Connector** can subscribe to a Kafka topic and write each message into an Elasticsearch index, making the data searchable.


#### Distributed vs. Standalone Mode

Kafka Connect can run in two modes :[^11_5]


| Mode | Description | Use Case |
| :-- | :-- | :-- |
| **Standalone Mode** | A single worker process runs all connectors and their tasks. Configuration is managed via local property files. | Development, testing, or scenarios where only a single agent is needed. Not fault-tolerant [^11_5]. |
| **Distributed Mode** | A cluster of workers run across multiple machines. Work is automatically balanced across the cluster. It provides scalability and fault tolerance. | **Production environments**. If a worker fails, its tasks are automatically reassigned to other workers in the cluster [^11_5]. |

* **Best Practice:** Always use **distributed mode** for production. It uses Kafka topics internally to store connector configurations, statuses, and offsets, making the cluster resilient. It also provides a REST API for managing connectors.[^11_4]

```bash
# Example REST API call to create a new connector in distributed mode
curl -X POST http://localhost:8083/connectors -H "Content-Type: application/json" -d '{
  "name": "jdbc-source-users",
  "config": {
    "connector.class": "io.confluent.connect.jdbc.JdbcSourceConnector",
    "connection.url": "jdbc:postgresql://localhost:5432/mydb",
    "topic.prefix": "db-users-",
    "mode": "incrementing",
    "incrementing.column.name": "id"
  }
}'
```


#### Common Connectors

A rich ecosystem of pre-built connectors exists. Some of the most popular are:

* **JDBC:** Generic connector for any database with a JDBC driver.
* **Debezium:** A powerful set of source connectors for Change Data Capture (CDC) from databases like MySQL, PostgreSQL, and MongoDB.
* **S3 Sink:** Dumps data from Kafka topics into files on Amazon S3 for long-term storage or big data analytics.
* **Elasticsearch Sink:** Indexes Kafka messages into Elasticsearch.


#### SMTs (Single Message Transforms)

Transforms are simple, pluggable components that can be chained together to make light modifications to messages as they pass through Kafka Connect.[^11_3]

* **Use Case:** You can use an SMT to add a static field, rename a field, filter out certain records, or change the topic a record is routed to, all without writing any code.
* **Example SMTs:**
    * `InsertField`: Add a static field and value.
    * `ReplaceField`: Rename or filter fields.
    * `TimestampRouter`: Route records to topics based on their timestamp.
* **Best Practice:** Use SMTs for simple, stateless data manipulation. For complex, stateful transformations, Kafka Streams is a more appropriate tool.


#### Offset Management and Resilience

* Kafka Connect automatically manages offsets for both source and sink connectors.
* For source connectors, it tracks the progress of what has been read from the source system (e.g., the last read primary key from a DB table).
* For sink connectors, it uses the standard Kafka consumer offset mechanism.
* This information is stored in an internal Kafka topic (`connect-offsets`), ensuring that if a connector is restarted, it can resume from where it left off.

***
Would you like to continue with the next section, "Schema Management"?
<span style="display:none">[^11_1][^11_7][^11_8][^11_9]</span>

<div style="text-align: center">⁂</div>

[^11_1]: https://docs.confluent.io/platform/current/connect/design.html

[^11_2]: https://www.instaclustr.com/blog/apache-kafka-connect-architecture-overview/

[^11_3]: https://www.redpanda.com/guides/kafka-tutorial-what-is-kafka-connect

[^11_4]: https://docs.confluent.io/platform/current/connect/index.html

[^11_5]: https://www.automq.com/blog/kafka-connect-architecture-concepts-best-practices

[^11_6]: https://developers.redhat.com/articles/2023/12/27/introduction-kafka-connect

[^11_7]: https://www.openlogic.com/blog/exploring-kafka-connect

[^11_8]: https://www.gridgain.com/docs/extensions/kafka/kc-architecture

[^11_9]: https://docs.snowflake.com/en/user-guide/kafka-connector-overview


---

# yes

You got it. Here is the revision guide for Section 11: Schema Management.

***

### 11. Schema Management

By default, Kafka treats messages as simple byte arrays, having no knowledge of their internal structure. This creates a "data contract" problem: how do you ensure producers and consumers agree on the data format, and how do you evolve that format without breaking applications? Schema management solves this.[^12_5]

#### Avro, JSON Schema, and Protobuf Support

These are the three most common schema formats used with Kafka.


| Format | Description | Strengths | Weaknesses |
| :-- | :-- | :-- | :-- |
| **Avro** | A data serialization system from the Hadoop ecosystem. Schemas are defined in JSON. | Excellent support for schema evolution. Compact binary format. Tightly integrated with the Kafka ecosystem. | Can be more verbose than Protobuf. |
| **Protobuf** | Protocol Buffers, developed by Google. Schemas are defined in `.proto` files. | Highly compact and efficient binary format. Strong typing and code generation in many languages. | Schema evolution rules are slightly less flexible than Avro's. |
| **JSON Schema** | A standard for validating the structure of JSON data. | Human-readable and easy to debug. Leverages the widespread use of JSON. | Not a binary format, so payloads are larger. Less efficient than Avro/Protobuf. |

* **Best Practice:** **Avro** is generally the recommended format for most Kafka use cases due to its superior schema evolution capabilities and native integration with tools like the Confluent Schema Registry.[^12_5]


#### Schema Registry Integration

A **Schema Registry** is a centralized, external service that stores a versioned history of all your schemas. It is not part of the Kafka brokers themselves.[^12_1][^12_6]

**How it works:**

1. **Producer:** Before sending a message, the producer's serializer checks if the message's schema is in the registry.
    * If not, it registers the schema and receives a unique integer **Schema ID**.
    * It then serializes the data and prepends the Schema ID to the message payload. The full schema is *not* sent with every message.
2. **Consumer:** When the consumer receives a message, its deserializer reads the Schema ID.
    * It asks the Schema Registry for the schema corresponding to that ID.
    * It uses that schema to correctly deserialize the message.
3. **Caching:** Both clients cache schemas locally, so they only need to contact the registry when they encounter a new Schema ID.[^12_6]

#### Schema Versioning and Compatibility Modes

The Schema Registry enforces **compatibility rules** when a new version of a schema is registered for a topic. This prevents producers from making changes that would break existing consumers.[^12_9]


| Compatibility Mode | Rule | Use Case |
| :-- | :-- | :-- |
| **`BACKWARD` (Default)** | Consumers using the new schema can read data produced with the last version of the schema. Allows you to *delete fields* or *add optional fields*. | The most common strategy. You upgrade consumers first, then producers. |
| **`FORWARD`** | Consumers using the last version of the schema can read data produced with the new schema. Allows you to *add required fields* (with defaults) or *delete optional fields*. | Less common. You upgrade producers first, then consumers. |
| **`FULL`** | The new schema is both backward and forward compatible. | Very restrictive. Ensures maximum compatibility but limits the types of changes you can make. |
| **`NONE`** | No compatibility checks are performed. | Disables the safety net. **Not recommended for production.** |

* **Common Pitfall:** Changing a field's data type (e.g., `string` to `int`) is almost always a breaking change and will be rejected by any compatibility mode other than `NONE`.


#### Best Practices for Schema Evolution

* **Field Additions:** When adding a new field, always provide a **default value**. This ensures that consumers using an older schema (which don't know about the new field) can still read new records, and consumers using the new schema can read old records (the new field will be populated with the default).
* **Field Deletions:** Only delete fields that are **optional** (i.e., not required). Deleting a required field will break backward compatibility.
* **Field Renaming:** Do not rename fields directly. Instead, add the new field and mark the old one as deprecated, or use **aliases** if your schema format (like Avro) supports them.

***
Would you like to continue with the next section, "Kafka Security"?
<span style="display:none">[^12_2][^12_3][^12_4][^12_7][^12_8]</span>

<div style="text-align: center">⁂</div>

[^12_1]: https://docs.confluent.io/platform/current/schema-registry/index.html

[^12_2]: https://www.ibm.com/think/insights/level-up-your-kafka-applications-with-schemas

[^12_3]: https://kafka.apache.org/documentation/

[^12_4]: https://oso.sh/blog/how-to-manage-schemas-in-apache-kafka/

[^12_5]: https://www.redpanda.com/guides/kafka-tutorial-kafka-schema-registry

[^12_6]: https://github.com/AutoMQ/automq/wiki/What-is-Kafka-Schema-Registry-Learn-\&-Use-\&Best-Practices

[^12_7]: https://cloud.google.com/managed-service-for-apache-kafka/docs/schema-registry/schema-registry-overview

[^12_8]: https://ibm.github.io/event-automation/es/schemas/overview/

[^12_9]: https://docs.confluent.io/platform/current/schema-registry/fundamentals/schema-evolution.html


---

# yes

Certainly. Here is the revision guide for Section 12: Kafka Security.

***

### 12. Kafka Security

Securing a Kafka cluster is critical, especially when it serves as the central data backbone for an organization. Kafka security rests on three pillars: Encryption, Authentication, and Authorization.[^13_5]

#### Encryption (TLS)

Encryption protects data from being intercepted and read by unauthorized parties.

* **Encryption in Transit:** This secures data moving between clients and brokers, and between brokers themselves. It is achieved using **TLS/SSL**.
    * **Configuration:** You configure listeners to use the `SSL` or `SASL_SSL` security protocol and provide truststores and keystores.[^13_5]
    * **Performance Impact:** While encryption and decryption require CPU power, the performance cost is typically negligible in a modern, optimized implementation.[^13_5]
* **Encryption at Rest:** Kafka does not provide built-in functionality for encrypting data on disk. This is typically handled at the infrastructure level through:
    * Disk-level encryption on the broker machines.
    * Using cloud provider services like AWS KMS or Azure Key Vault for managed keys and encrypted volumes.[^13_5]


#### Authentication (SSL/SASL)

Authentication verifies the identity of a client (a producer, consumer, or another broker) connecting to the cluster.[^13_2]

* **mTLS (Mutual TLS Authentication):** Both the client and server present SSL certificates to each other to verify their identities. This is a strong, certificate-based authentication method.
* **SASL (Simple Authentication and Security Layer):** A framework that supports multiple authentication mechanisms. This is the most common approach.[^13_5]
    * `SASL/PLAIN`: Simple username/password authentication. **It must be used with SSL** to prevent sending credentials in cleartext.
    * `SASL/SCRAM`: A more secure challenge-response mechanism for passwords that avoids sending the password directly. **This is a common best practice**.[^13_5]
    * `SASL/GSSAPI`: Integrates with Kerberos for authentication in environments that already use it.
    * `SASL/OAUTHBEARER`: Uses OAuth 2.0 tokens for authentication, suitable for modern cloud-native applications.

**Client Configuration Example (Java - SASL/SCRAM):**

```java
Properties props = new Properties();
props.put("bootstrap.servers", "broker1:9094");
props.put("security.protocol", "SASL_SSL");
props.put("sasl.mechanism", "SCRAM-SHA-256");
props.put("sasl.jaas.config", "org.apache.kafka.common.security.scram.ScramLoginModule required " +
          "username=\"my-user\" password=\"my-secret\";");
```


#### ACLs and Authorization

Once a client is authenticated, **authorization** determines what actions that client is allowed to perform. Kafka uses **Access Control Lists (ACLs)** for this.[^13_2]

* An ACL is a rule that grants a permission (`Allow` or `Deny`) to a principal (user) for a specific operation (e.g., `Read`, `Write`) on a resource (e.g., a topic, consumer group, or the cluster itself).

**Example using `kafka-acls.sh`:**

```bash
# Allow 'user1' to write to 'topic-A'
kafka-acls.sh --bootstrap-server localhost:9094 --add \
  --allow-principal User:user1 \
  --operation Write \
  --topic topic-A

# Allow 'group1' to read from 'topic-A'
kafka-acls.sh --bootstrap-server localhost:9094 --add \
  --allow-principal User:consumer-app \
  --operation Read \
  --group group1 \
  --topic topic-A
```

* **Best Practice:** Follow the **principle of least privilege**. Only grant the permissions absolutely necessary for an application to function.[^13_5]
* **Common Pitfall:** In production, always set `allow.everyone.if.no.acl.found=false` on the brokers. This ensures that access is denied by default unless an explicit ACL grants it.[^13_5]


#### Kafka Audit Logging

While not enabled by default, Kafka can be configured to produce audit logs using Log4j. These logs provide a record of all authentication and authorization successes and failures, which is crucial for security monitoring and compliance. You can track who accessed what resource, when, and from where.[^13_2]

***
Would you like to continue with the next section, "Monitoring and Observability"?
<span style="display:none">[^13_1][^13_3][^13_4][^13_6][^13_7][^13_8]</span>

<div style="text-align: center">⁂</div>

[^13_1]: https://kafka.apache.org/10/documentation/streams/developer-guide/security.html

[^13_2]: https://www.confluent.io/blog/kafka-security-how-to-secure-real-time-data-streams/

[^13_3]: https://kafka.apache.org/project-security

[^13_4]: https://tuxcare.com/blog/apache-kafka-security/

[^13_5]: https://www.automq.com/blog/kafka-security-all-you-need-to-know-and-best-practices

[^13_6]: https://developer.ibm.com/tutorials/kafka-authn-authz/

[^13_7]: https://www.slideshare.net/slideshow/apache-kafka-security-overview/238896043

[^13_8]: https://www.instaclustr.com/education/apache-kafka/hosted-apache-kafka-features-to-look-for-and-4-key-considerations/


---

# yes

Of course. Here is the revision guide for Section 13: Monitoring and Observability.

***

### 13. Monitoring and Observability

Monitoring a Kafka cluster is not optional; it's essential for ensuring reliability, optimizing performance, and troubleshooting issues before they cause an outage. Effective monitoring involves tracking key metrics from brokers, producers, and consumers.[^14_4]

#### Key Metrics to Monitor

Metrics in Kafka are exposed via JMX (Java Management Extensions) and can be scraped by monitoring systems.[^14_2]

**Broker Metrics (Cluster Health):**

* **`UnderReplicatedPartitions`**: The number of partitions that do not have their target number of in-sync replicas. **This is the single most important metric for cluster health.** A value greater than 0 indicates a problem (e.g., a broker is down or slow).[^14_3][^14_6]
* **`IsrShrinksPerSec` / `IsrExpandsPerSec`**: The rate at which the In-Sync Replica (ISR) set for partitions is shrinking or expanding. Frequent shrinks can signal an unstable network or overloaded brokers.[^14_6]
* **`ActiveControllerCount`**: Should be exactly 1 in a healthy cluster.[^14_6]
* **`OfflinePartitionsCount`**: Should be 0. Any value greater than 0 means data is unavailable for those partitions.[^14_6]
* **Resource Utilization**: Monitor broker CPU usage, disk space, and network I/O. A sudden spike or maxed-out resource is a clear sign of a bottleneck.[^14_5]

**Producer Metrics (Ingestion Health):**

* **`record-error-rate`**: The rate of records that failed to be sent. Should be 0.
* **`request-latency-avg`**: The average time for a produce request to be acknowledged. A rising latency can indicate broker or network issues.
* **`batch-size-avg`**: The average batch size. If this is consistently low, you may need to tune `linger.ms` to improve throughput.

**Consumer Metrics (Consumption Health):**

* **`records-lag-max`**: The maximum lag (difference in offsets) between a consumer and the end of a partition. **This is the most critical consumer metric.** It shows how far behind a consumer group is. A continuously growing lag is a sign that consumers cannot keep up with producers.[^14_4]
* **`fetch-rate`**: The rate at which consumers are fetching messages. A drop can indicate a consumer-side processing issue.
* **`records-consumed-rate`**: The rate at which records are being processed. This, combined with lag, gives a full picture of consumer performance.[^14_5]


#### Prometheus \& Grafana Dashboards

The most common open-source stack for Kafka monitoring involves Prometheus for collecting and storing time-series metrics, and Grafana for visualizing them in dashboards.[^14_7]

* **Setup:** You deploy an "exporter" alongside your Kafka brokers (e.g., JMX Exporter or Kafka Exporter) which exposes the JMX metrics in a format Prometheus can scrape.[^14_4]
* **Dashboards:** Pre-built Grafana dashboards are widely available, providing visualizations for all the key metrics mentioned above, often with alerting rules already configured.


#### Monitoring Tools

| Tool | Description | Use Case |
| :-- | :-- | :-- |
| **Prometheus \& Grafana** | Open-source standard for metrics collection and visualization. Highly flexible and powerful. | General-purpose monitoring and alerting for any infrastructure, including Kafka [^14_7]. |
| **CMAK (Kafka Manager)** | A web-based UI for managing and monitoring Kafka clusters. Provides a high-level overview. | Good for administrative tasks (topic creation, partition rebalancing) and basic monitoring of cluster health and consumer groups [^14_7]. |
| **Confluent Control Center** | A comprehensive, web-based UI for managing and monitoring Kafka, part of the Confluent Platform. | Offers deep insights into data streams, ksqlDB, and connectors. Best suited for users of the Confluent ecosystem. |
| **Burrow** | An open-source tool specifically for monitoring consumer lag. | Provides detailed consumer group status and lag checking as a service, often with HTTP endpoints for integration. |


***
Would you like to continue with the next section, "Kafka in Production"?
<span style="display:none">[^14_1][^14_10][^14_8][^14_9]</span>

<div style="text-align: center">⁂</div>

[^14_1]: https://kafka.apache.org/documentation/

[^14_2]: https://docs.confluent.io/platform/current/kafka/monitoring.html

[^14_3]: https://middleware.io/blog/kafka-monitoring/

[^14_4]: https://www.redpanda.com/guides/kafka-performance-kafka-monitoring

[^14_5]: https://lumigo.io/blog/essential-metrics-for-kafka-performance-monitoring/

[^14_6]: https://www.datadoghq.com/blog/monitoring-kafka-performance-metrics/

[^14_7]: https://www.instaclustr.com/education/apache-kafka/kafka-monitoring-key-metrics-and-5-tools-to-know-in-2025/

[^14_8]: https://logit.io/blog/post/kafka-monitoring-tools/

[^14_9]: https://www.dynatrace.com/hub/detail/apache-kafka/

[^14_10]: https://www.manageengine.com/products/applications_manager/help/kafka-monitoring-tools.html


---

# yes

Absolutely. Here is the revision guide for Section 14: Kafka in Production.

***

### 14. Kafka in Production

Running Kafka in production requires careful planning around deployment, configuration, and operational procedures to ensure high availability, durability, and performance.

#### Partitioning and Replication Strategies

* **Partitioning:** The number of partitions is the primary lever for parallelism.
    * **Best Practice:** Over-partition to a reasonable degree. It's easier to add consumer instances to handle more partitions than it is to add partitions to a topic later (as this can disrupt key-based ordering). A good starting point is to estimate your target throughput and the throughput of a single consumer instance.
* **Replication:** Always use a replication factor of at least **3** for production topics. This allows the cluster to tolerate the failure of one broker without data loss and another broker being down for maintenance.
* **`min.insync.replicas`:** For critical topics, set this to **2**. This, combined with `replication.factor=3` and producer `acks=all`, ensures that every write is confirmed by at least two brokers before being acknowledged, providing a strong durability guarantee.


#### ISR and Replica Placement

* **Replica Placement:** Kafka's default replica placement strategy attempts to spread replicas of a partition across different racks (if configured) or brokers. This is crucial for availability.
* **Rack Awareness:** If your brokers span multiple physical racks or cloud availability zones (AZs), configure `broker.rack` in `server.properties`. This tells Kafka to make a best effort to place replicas for a given partition in different racks/AZs. If one AZ goes down, the topic remains available.


#### Rolling Upgrades and Downtime Minimization

Kafka is designed to be upgraded without downtime.

* **Procedure:** Upgrade one broker at a time.

1. Shut down the broker cleanly.
2. Upgrade its software.
3. Restart the broker.
4. Wait for it to fully rejoin the cluster and for all its partitions to be in the ISR (monitor `UnderReplicatedPartitions` metric).
5. Move to the next broker.
* **Best Practice:** Always upgrade ZooKeeper/KRaft controllers *before* upgrading the brokers. Read the official upgrade notes for the specific Kafka version, as there may be required changes to `inter.broker.protocol.version`.


#### Handling Message Backlog and Lag

* **Monitoring Lag:** Continuously monitor the `records-lag-max` metric for all consumer groups. Set up alerts for when lag exceeds a certain threshold.
* **Scaling Consumers:** If lag is consistently growing, the primary solution is to add more consumer instances to the group (up to the number of partitions).
* **Tuning Consumers:** You can also tune consumers to fetch and process records faster by increasing `fetch.min.bytes` and `max.poll.records`, provided the processing logic can handle larger batches.
* **Best Practice:** If a consumer group falls hopelessly behind, you may need to decide whether to skip the backlog and reset its offset to the latest, or to provision a temporary, large group of consumers to burn down the backlog quickly.


#### Retention and Compaction Tuning

* **Topic-Level Retention:** Do not rely on the global broker-level retention settings. Define `retention.ms` for each topic based on its specific requirements.[^15_2]
* **Storage Planning:** Calculate your storage needs based on your average message size, ingress rate, and retention period. Provision disk space accordingly, with a healthy buffer for growth and spikes.
* **Compaction:** For compacted topics, ensure the Log Cleaner is running efficiently. Monitor its performance and ensure the heap space allocated to it is sufficient. If compaction can't keep up, the log will grow indefinitely.

***
Would you like to continue with the next section, "Kafka Performance Optimization"?
<span style="display:none">[^15_1][^15_3][^15_4][^15_5][^15_6][^15_7][^15_8]</span>

<div style="text-align: center">⁂</div>

[^15_1]: https://docs.confluent.io/platform/current/kafka/post-deployment.html

[^15_2]: https://www.instaclustr.com/education/apache-kafka/12-kafka-best-practices-run-kafka-like-the-pros/

[^15_3]: https://docs.confluent.io/platform/current/kafka/deployment.html

[^15_4]: https://stackoverflow.com/questions/65955521/what-is-the-recommended-production-deployment-strategy-for-apache-kafka

[^15_5]: https://github.com/AutoMQ/automq/wiki/Kafka-on-Kubernetes:-Deployment-\&-Best-Practices

[^15_6]: https://blog.opensight.ch/kafka-in-production-building-a-scalable-secure-and-enterprise-ready-event-bus-2/

[^15_7]: https://stackoverflow.blog/2024/09/04/best-practices-for-cost-efficient-kafka-clusters/

[^15_8]: https://www.kai-waehner.de/blog/2024/07/29/apache-kafka-cluster-type-deployment-strategies/


---

# yes

Of course. Here is the revision guide for Section 15: Kafka Performance Optimization.

***

### 15. Kafka Performance Optimization

Optimizing Kafka is a balancing act between throughput, latency, durability, and cost. The right strategy depends entirely on your specific use case. The goal is to identify and eliminate bottlenecks, whether they are in the producers, consumers, or the brokers themselves.[^16_1]

#### Producer Throughput Tuning

The key to high producer throughput is sending fewer, larger requests. This is achieved by batching.[^16_2]


| Parameter | Description \& Recommendation |
| :-- | :-- |
| **`batch.size`** | The maximum size of a batch of records. The default (16KB) is often too small for high-throughput workloads. Increase this to 32KB, 64KB, or even higher to improve efficiency [^16_3]. |
| **`linger.ms`** | The time a producer will wait for a batch to fill up before sending it. The default is 0 (no waiting). Setting this to 5-20ms encourages the producer to create larger batches, significantly boosting throughput at the cost of a small increase in latency [^16_3]. |
| **`compression.type`** | Compressing batches reduces network traffic and storage size. `lz4` and `zstd` offer excellent performance with low CPU overhead. This is almost always a good idea for text-based data like JSON [^16_2]. |
| **`buffer.memory`** | The total memory available for the producer to buffer records waiting to be sent. Ensure this is large enough to accommodate the configured `batch.size` and the number of in-flight requests. |

#### Consumer Tuning for High Poll Volumes

Consumer performance is about fetching data efficiently and processing it quickly.

* **Balance `fetch.min.bytes` and `fetch.max.wait.ms`**:
    * `fetch.min.bytes` tells the broker to wait until it has at least this much data before responding to a fetch request. Increasing this reduces the number of requests and broker load.
    * `fetch.max.wait.ms` is the timeout for that wait.
    * **For high throughput**, increase `fetch.min.bytes` (e.g., 50KB) and `fetch.max.wait.ms` (e.g., 500ms).
    * **For low latency**, decrease both.[^16_1]
* **Adjust `max.poll.records`**: This controls how many records your consumer gets in a single `poll()` call. The right value depends on how long it takes to process a single record. If your processing is slow, a smaller value prevents the consumer from timing out of the group (`max.poll.interval.ms`).[^16_1]
* **Parallelism**: The most effective way to increase consumption speed is to increase the number of partitions on the topic and run an equal number of consumer instances in the group.


#### Broker I/O Optimization

Kafka is heavily dependent on disk I/O performance.

* **Use SSDs:** Solid-State Drives (SSDs) provide significantly lower latency for disk I/O compared to spinning disks (HDDs). For latency-sensitive workloads, SSDs are critical.[^16_2]
* **Multiple `log.dirs`**: If using HDDs, configure `log.dirs` with a comma-separated list of paths on different physical disks. Kafka will stripe partitions across these disks, parallelizing the I/O load.
* **Avoid Network-Attached Storage (NAS):** NAS can introduce unpredictable network latency, which is a "silent performance killer". Always prefer locally attached disks.[^16_5]


#### Page Cache Usage and OS Tuning

Kafka is designed to leverage the OS page cache for both reads and writes.

* **Give Memory to the OS, Not the JVM:** Do not allocate a massive heap to the Kafka JVM. A moderate heap (e.g., 6-8 GB) is usually sufficient. The remaining system RAM should be left free for the OS to use as a page cache. A large page cache means more reads and writes can be served from memory, avoiding slow disk access.
* **File System:** Use a modern filesystem like XFS or ext4.
* **Increase File Descriptors:** Kafka uses a large number of file handles. Increase the OS limit (`ulimit -n`) to a high value like 100,000 for the Kafka user.

***
Would you like to continue with the next section, "Spring Boot with Kafka"?
<span style="display:none">[^16_4][^16_6][^16_7][^16_8][^16_9]</span>

<div style="text-align: center">⁂</div>

[^16_1]: https://www.redpanda.com/guides/kafka-performance-kafka-performance-tuning

[^16_2]: https://www.instaclustr.com/education/apache-kafka/kafka-performance-7-critical-best-practices/

[^16_3]: https://www.redpanda.com/guides/kafka-performance-kafka-optimization

[^16_4]: https://www.intel.com/content/www/us/en/developer/articles/guide/kafka-optimization-and-benchmarking-guide.html

[^16_5]: https://www.meshiq.com/top-10-tips-for-tuning-kafka-performance/

[^16_6]: https://developers.redhat.com/articles/2022/05/03/fine-tune-kafka-performance-kafka-optimization-theorem

[^16_7]: https://learn.microsoft.com/en-us/azure/hdinsight/kafka/apache-kafka-performance-tuning

[^16_8]: https://developer.confluent.io/learn/kafka-performance/

[^16_9]: https://www.ksolves.com/blog/big-data/kafka-optimization-tips


---

# yes

You've got it. Here is the revision guide for Section 16: Spring Boot with Kafka.

***

### 16. Spring Boot with Kafka

Spring for Apache Kafka (`spring-kafka`) provides a high-level abstraction over the native Kafka client libraries, making it significantly easier to build messaging applications within the Spring ecosystem. Spring Boot further simplifies this with auto-configuration and a declarative, annotation-based approach.[^17_3][^17_5]

#### `KafkaTemplate` and `MessageListenerContainer`

These are the two central components for producing and consuming messages.

* **`KafkaTemplate` (Producer):** A wrapper around the `KafkaProducer` that simplifies sending messages. It handles thread safety and provides convenient methods for sending data.[^17_6]

**Real-World Example (Sending a message):**

```java
@Service
public class OrderProducer {

    @Autowired
    private KafkaTemplate<String, OrderEvent> kafkaTemplate;

    public void sendOrder(OrderEvent order) {
        kafkaTemplate.send("orders-topic", order.getOrderId(), order);
    }
}
```

* **`@KafkaListener` (Consumer):** An annotation that marks a method as the target for a Kafka message listener container. Spring Boot automatically configures the underlying `MessageListenerContainer` to poll for messages and invoke your method.[^17_4]

**Real-World Example (Receiving a message):**

```java
@Service
public class OrderConsumer {

    @KafkaListener(topics = "orders-topic", groupId = "inventory-service")
    public void listenForOrders(OrderEvent order) {
        System.out.println("Received Order: " + order.getOrderId());
        // Process the order...
    }
}
```


#### Declarative Kafka Config via YAML/Properties

Spring Boot allows you to configure nearly all producer and consumer properties in your `application.yml` or `application.properties` file, removing the need for verbose configuration beans.[^17_5]

**Real-World Example (`application.yml`):**

```yaml
spring:
  kafka:
    bootstrap-servers: localhost:9092
    producer:
      key-serializer: org.apache.kafka.common.serialization.StringSerializer
      value-serializer: org.springframework.kafka.support.serializer.JsonSerializer
      properties:
        acks: all
        compression.type: snappy
    consumer:
      group-id: my-application
      auto-offset-reset: earliest
      key-deserializer: org.apache.kafka.common.serialization.StringDeserializer
      value-deserializer: org.springframework.kafka.support.serializer.JsonDeserializer
      properties:
        spring.json.trusted.packages: "com.example.events.*" # Required for JSON deserialization
        max.poll.interval.ms: 300000
```


#### Spring Retry and Error Handling

Spring for Kafka provides robust error handling capabilities.

* **Retries:** You can easily add retry logic for transient errors using Spring Retry. By annotating a `@KafkaListener` with `@RetryableTopic`, Spring will automatically create retry topics and a Dead Letter Topic (DLT).

**Real-World Example (Retryable Listener):**

```java
@RetryableTopic(
    attempts = "3", // Attempt to process the message 3 times
    backoff = @Backoff(delay = 1000, multiplier = 2.0), // Exponential backoff
    dltStrategy = DltStrategy.FAIL_ON_ERROR // After all retries fail, stop processing
)
@KafkaListener(topics = "orders-topic", groupId = "inventory-service")
public void listenWithRetry(OrderEvent order) {
    // ... processing logic that might fail
}
```

* **Dead Letter Topics (DLT):** When a message fails processing even after all retry attempts, it is sent to a Dead Letter Topic. The message is enriched with headers containing information about the failure (original topic, exception message, stack trace), allowing for later analysis and manual intervention.


#### Transaction Support in Spring Kafka

Spring provides excellent support for Kafka transactions.

* You can configure a `KafkaTransactionManager` and use Spring's standard `@Transactional` annotation on methods that use `KafkaTemplate`.
* This ensures that all `kafkaTemplate.send()` operations within the method are part of a single, atomic Kafka transaction.
* For a "read-process-write" pattern, you can configure the listener container to run in transactional mode. The consumer offsets will be committed as part of the same transaction as the producer's writes.

***
Would you like to continue with the next section, "Integration Patterns"?
<span style="display:none">[^17_1][^17_2][^17_7][^17_8]</span>

<div style="text-align: center">⁂</div>

[^17_1]: https://www.geeksforgeeks.org/advance-java/spring-boot-integration-with-kafka/

[^17_2]: https://javatechonline.com/how-to-work-with-apache-kafka-in-spring-boot/

[^17_3]: https://spring.io/projects/spring-kafka

[^17_4]: https://www.instaclustr.com/education/apache-kafka/spring-boot-with-apache-kafka-tutorial-and-best-practices/

[^17_5]: https://www.confluent.io/learn/spring-boot-kafka/

[^17_6]: https://www.tutorialspoint.com/spring_boot/spring_boot_apache_kafka.htm

[^17_7]: https://www.baeldung.com/spring-kafka

[^17_8]: https://www.youtube.com/watch?v=SqVfCyfCJqw


---

# yes

Of course. Here is the revision guide for Section 17: Integration Patterns.

***

### 17. Integration Patterns

Kafka's unique design as a durable, distributed log enables powerful integration patterns that are central to modern, decoupled architectures.[^18_4]

#### Event-Driven Architecture with Kafka

This is the most fundamental pattern. Instead of services making direct, synchronous requests to each other, they communicate asynchronously by producing and consuming **events**.

* **How it works:** An `Order Service` doesn't call the `Notification Service` and `Inventory Service` directly. Instead, it publishes an `OrderCreated` event to a Kafka topic. Both downstream services subscribe to this topic and react to the event independently.
* **Benefits:**
    * **Loose Coupling:** Services don't need to know about each other. You can add, remove, or change a service without impacting others.
    * **Resilience:** If the `Notification Service` is down, the events queue up in Kafka. It can process them when it comes back online, and the `Order Service` is unaffected.
    * **Scalability:** Each service can be scaled independently.


#### Event Sourcing

In this pattern, the state of an application is not stored as its current form in a database. Instead, the application stores the full sequence of events that have ever happened. Kafka is the perfect system to act as this **event store**.

* **How it works:** To determine a customer's current account balance, you don't look up a value in a table. You replay all the `Deposit` and `Withdrawal` events for that customer from a Kafka topic.
* **Benefits:**
    * **Complete Audit Trail:** You have a perfect, immutable history of everything that ever happened.
    * **Temporal Queries:** You can reconstruct the state of the system at any point in time.
    * **Flexibility:** You can create new "projections" or views of the data at any time by re-processing the event log.


#### CQRS (Command Query Responsibility Segregation)

CQRS is a pattern that separates the models used for writing data (Commands) from the models used for reading data (Queries). Kafka is often the bridge between the two sides.

* **How it works:**

1. The "Command" side of the application handles requests that change state (e.g., `CreateOrderCommand`) and writes events to Kafka.
2. A separate "Query" side consists of consumers that listen to these events and build optimized "read models" (e.g., in Elasticsearch or a relational database) designed specifically for fast querying.
* **Benefits:** Each side can be scaled and optimized independently for its specific task. The write side is optimized for transactional consistency, while the read side is optimized for query performance.


#### CDC (Change Data Capture) with Kafka and Debezium

CDC is the process of capturing row-level changes from a database (inserts, updates, deletes) and streaming them as events.

* **How it works:** You deploy a **Debezium** connector (via Kafka Connect) that tails the transaction log of your database (e.g., MySQL's binlog). It converts each database change into an event and publishes it to a Kafka topic.
* **Use Case:** This is an incredibly powerful way to unlock data from legacy monolithic databases and make it available to microservices and real-time analytics platforms without modifying the original application.


#### Outbox Pattern

This pattern solves the problem of reliably updating a database and publishing an event as a single atomic operation.

* **How it works:**

1. When handling a request, an application service performs its database writes and, within the *same local database transaction*, inserts an event record into an "outbox" table.
2. A separate Debezium connector (or a custom process) monitors this outbox table.
3. When a new record appears in the outbox, the connector publishes it to Kafka.
* **Benefit:** This guarantees that an event is published **if and only if** the database transaction commits successfully, preventing inconsistencies between your service's state and the events it broadcasts.

***
Would you like to continue with the next section, "Cloud \& Kubernetes Deployments"?
<span style="display:none">[^18_1][^18_2][^18_3][^18_5][^18_6][^18_7][^18_8]</span>

<div style="text-align: center">⁂</div>

[^18_1]: https://www.smily.com/engineering/integration-patterns-for-distributed-architecture-intro-to-kafka

[^18_2]: https://www.instaclustr.com/education/apache-kafka/apache-kafka-integration-challenges-solutions-and-best-practices/

[^18_3]: https://dzone.com/refcardz/apache-kafka-patterns-and-anti-patterns

[^18_4]: https://www.linkedin.com/pulse/kafka-integration-patterns-exploring-common-architectures-integrating-6ns8c

[^18_5]: https://www.enterpriseintegrationpatterns.com/patterns/messaging/CompetingConsumers.html

[^18_6]: https://stackoverflow.blog/2022/07/21/event-driven-topic-design-using-kafka/

[^18_7]: https://estuary.dev/blog/kafka-event-driven-architecture/

[^18_8]: https://spark.apache.org/docs/latest/structured-streaming-kafka-integration.html


---

# yes

Certainly. Here is the revision guide for Section 18: Cloud \& Kubernetes Deployments.

***

### 18. Cloud \& Kubernetes Deployments

Deploying Kafka in the cloud offers flexibility and scalability, but also introduces unique challenges. You can choose between fully managed services or self-managing Kafka on cloud infrastructure, most commonly on Kubernetes.[^19_5]

#### Managed Kafka Services

These services abstract away the complexity of managing the underlying infrastructure, allowing you to focus on your applications.


| Service | Provider | Description |
| :-- | :-- | :-- |
| **Amazon MSK** | AWS | A fully managed Apache Kafka service. It handles provisioning, configuration, and maintenance of Kafka clusters, including features for high availability across multiple Availability Zones (AZs) [^19_5]. |
| **Azure Event Hubs** | Microsoft | A highly scalable data streaming platform with a Kafka-compatible API. While not running actual Kafka brokers, it allows you to use your existing Kafka applications with minimal code changes. |
| **Google Cloud Pub/Sub** | GCP | Similar to Event Hubs, Pub/Sub offers a Kafka-compatible interface (Pub/Sub Lite) that allows Kafka clients to connect to a serverless messaging backbone. |
| **Confluent Cloud** | Confluent | A fully managed, cloud-native Kafka service available on AWS, Azure, and GCP. It provides the complete Confluent Platform, including ksqlDB, Schema Registry, and various connectors. |

* **Best Practice:** For most teams starting out, a **managed service** is the recommended approach. It significantly reduces operational overhead and provides built-in reliability and security features.


#### Kafka on Kubernetes with Strimzi

Running Kafka on Kubernetes gives you more control than a managed service but is significantly more complex. The main challenge is that Kafka is a stateful application, while Kubernetes excels at managing stateless ones.[^19_7]

* **Strimzi:** An open-source project that simplifies deploying and running Kafka on Kubernetes. It uses the **Operator pattern**.[^19_7]
    * You install the Strimzi Operator in your cluster.
    * You then define your Kafka cluster, topics, users, and connectors as simple declarative YAML files (Custom Resources).
    * The Operator watches these resources and automatically provisions and manages the necessary Kubernetes objects (StatefulSets, Services, ConfigMaps, etc.) to make your desired state a reality.

**Real-World Example (Strimzi Custom Resource for a Kafka cluster):**

```yaml
apiVersion: kafka.strimzi.io/v1beta2
kind: Kafka
metadata:
  name: my-cluster
spec:
  kafka:
    version: 3.7.0
    replicas: 3
    listeners:
      - name: plain
        port: 9092
        type: internal
        tls: false
      - name: tls
        port: 9093
        type: internal
        tls: true
    storage:
      type: jbod # Just a bunch of disks
      volumes:
        - id: 0
          type: persistent-claim
          size: 100Gi
          deleteClaim: false
  zookeeper:
    replicas: 3
    storage:
      type: persistent-claim
      size: 100Gi
      deleteClaim: false
```


#### Helm Charts and Operators

* **Helm Charts:** A simpler way to get started. Helm is a package manager for Kubernetes, and charts exist for deploying Kafka. However, Helm mainly handles initial installation and doesn't help with Day 2 operations (like upgrades, rebalancing, or failure recovery).[^19_6]
* **Operators (like Strimzi):** The preferred method for production. Operators encode operational knowledge into software, automating complex tasks like rolling upgrades, certificate management, and broker scaling.[^19_7]


#### Networking Considerations in Cloud/K8s

This is one of the most complex aspects.

* **Internal Communication:** Brokers need to discover and talk to each other. In Kubernetes, this is typically handled via a headless service.
* **External Communication:** Clients outside the Kubernetes cluster need a way to connect. Common solutions include:
    * `NodePort`: Exposes the brokers on a port on each Kubernetes node.
    * `LoadBalancer`: Provisions a cloud load balancer for each broker. Can be expensive.
    * `Ingress`: Uses an Ingress controller to route external traffic, often more complex to configure for Kafka.
* **`advertised.listeners`:** This Kafka configuration must be set correctly so that clients, wherever they are, are given the right address to connect to a broker. Strimzi handles this configuration automatically.

***
Would you like to continue with the next section, "KRaft Mode (No ZooKeeper)"?
<span style="display:none">[^19_1][^19_2][^19_3][^19_4][^19_8][^19_9]</span>

<div style="text-align: center">⁂</div>

[^19_1]: https://docs.confluent.io/platform/current/kafka/post-deployment.html

[^19_2]: https://www.instaclustr.com/education/apache-kafka/12-kafka-best-practices-run-kafka-like-the-pros/

[^19_3]: https://www.confluent.io/blog/design-and-deployment-considerations-for-deploying-apache-kafka-on-aws/

[^19_4]: https://www.kai-waehner.de/blog/2024/07/29/apache-kafka-cluster-type-deployment-strategies/

[^19_5]: https://www.redpanda.com/guides/kafka-cloud

[^19_6]: https://github.com/AutoMQ/automq/wiki/Kafka-Operator:-Deployment-\&-Best-Practices

[^19_7]: https://www.automq.com/blog/kafka-on-kubernetes-deployment-best-practices

[^19_8]: https://stackoverflow.blog/2024/09/04/best-practices-for-cost-efficient-kafka-clusters/

[^19_9]: https://www.instaclustr.com/education/apache-kafka/apache-kafka-integration-challenges-solutions-and-best-practices/


---

# yes

Absolutely. Here is the revision guide for Section 19: KRaft Mode (No ZooKeeper).

***

### 19. KRaft Mode (No ZooKeeper)

KRaft (Kafka Raft) is a major architectural evolution that removes Kafka's dependency on Apache ZooKeeper. By integrating metadata management directly into Kafka using the Raft consensus protocol, KRaft simplifies architecture, improves performance, and increases scalability.[^20_1][^20_2][^20_7]

#### Metadata Quorum Controller

In KRaft mode, the role of managing cluster metadata is taken over from ZooKeeper by a quorum of Kafka nodes acting as **controllers**.[^20_1]

* **How it works:** A subset of nodes in the cluster (typically 3 or 5 for production) are designated with the `controller` role. These nodes form a "quorum" and use the Raft protocol to elect a single active controller and replicate metadata amongst themselves.[^20_5]
* **Metadata Topic:** All cluster metadata (broker status, topic configurations, ACLs) is stored in an internal, highly replicated Kafka topic called `__cluster_metadata`. The active controller writes to this log, and other controllers and brokers consume from it.[^20_5]
* This event-sourced model allows for extremely fast controller failover, as a new leader already has all the committed metadata in memory and can take over almost instantly.[^20_1]


#### Migration from ZooKeeper to KRaft

Migrating an existing ZooKeeper-based cluster to KRaft is a delicate process that is being rolled out through various KIPs (Kafka Improvement Proposals).[^20_1]

* The general process involves running the cluster in a "migration mode," where brokers can communicate with both ZooKeeper and the new KRaft controllers.
* Once all metadata has been successfully migrated from ZooKeeper to the KRaft controller quorum, the cluster can be switched to run exclusively in KRaft mode, and the ZooKeeper ensemble can be decommissioned.
* **Kafka Version Note:** Full migration tooling is a key feature in recent Kafka versions (3.x). Always consult the official documentation for the specific version you are running before attempting a migration.


#### Pros, Cons, and Operational Differences

| Aspect | KRaft Mode | ZooKeeper Mode |
| :-- | :-- | :-- |
| **Simplicity** | **Simpler.** Single system to deploy, manage, secure, and monitor. Fewer moving parts [^20_7]. | **More Complex.** Requires managing a separate, distributed ZooKeeper cluster with its own operational overhead. |
| **Scalability** | **Higher.** Can support millions of partitions in a single cluster, as metadata propagation is more efficient. | **Limited.** ZooKeeper can become a bottleneck in very large clusters with frequent metadata changes. |
| **Recovery Time** | **Faster.** Controller failover is nearly instantaneous (sub-second), improving cluster availability [^20_5]. | **Slower.** Controller failover requires reading state from ZooKeeper, which can take several seconds or more. |
| **Infrastructure** | Can run in "combined" mode (broker+controller on same node) for small setups, or "isolated" mode (dedicated controller nodes) for production [^20_1]. | Always requires a separate set of servers for the ZooKeeper ensemble. |

#### Current Status and Production Readiness

* KRaft mode has been considered **production-ready** for new clusters since Apache Kafka version **3.3**.[^20_1]
* Kafka 4.0, a major upcoming release, will **completely remove** support for ZooKeeper mode. All new development and features are focused on the KRaft architecture.[^20_6]
* **Best Practice:** All new Kafka deployments should use KRaft mode. Teams with existing ZooKeeper-based clusters should begin planning their migration strategy.

**Configuration Example (`server.properties` for a KRaft node):**

```properties
# Node 1 in a 3-node controller quorum
process.roles=broker,controller
node.id=1
controller.quorum.voters=1@localhost:9093,2@kafka2:9093,3@kafka3:9093
listeners=PLAINTEXT://:9092,CONTROLLER://:9093
```


***
Would you like to continue with the next section, "Tiered Storage"?
<span style="display:none">[^20_3][^20_4][^20_8][^20_9]</span>

<div style="text-align: center">⁂</div>

[^20_1]: https://developer.confluent.io/learn/kraft/

[^20_2]: https://www.redpanda.com/guides/kafka-tutorial-kafka-without-zookeeper

[^20_3]: https://learn.conduktor.io/kafka/how-to-install-apache-kafka-on-linux-without-zookeeper-kraft-mode/

[^20_4]: https://www.baeldung.com/kafka-shift-from-zookeeper-to-kraft

[^20_5]: https://hevodata.com/learn/kafka-without-zookeeper/

[^20_6]: https://www.openlogic.com/blog/kafka-raft-mode

[^20_7]: https://www.instaclustr.com/education/apache-spark/running-apache-kafka-kraft-on-docker-tutorial-and-best-practices/

[^20_8]: https://kafka.apache.org/41/documentation/zk2kraft.html

[^20_9]: https://learn.conduktor.io/kafka/how-to-install-apache-kafka-on-mac-without-zookeeper-kraft-mode/


---

# yes

You've got it. Here is the revision guide for Section 20: Tiered Storage.

***

### 20. Tiered Storage

Tiered Storage is a fundamental architectural shift in Kafka designed to decouple compute and storage, primarily to reduce costs and enable long-term data retention. It allows Kafka to use cheaper object storage (like AWS S3) for historical data while keeping recent, "hot" data on fast local disks.[^21_1][^21_2][^21_6]

#### Introduction and Use Cases (KIP-405)

The core problem that Tiered Storage solves is that in traditional Kafka, storage and compute are tightly coupled. To increase your data retention (i.e., add more storage), you have to add more brokers, which also adds compute capacity you may not need. This makes storing data in Kafka for long periods prohibitively expensive.[^21_5]

* **Use Cases:**
    * **Infinite Retention:** Store data in Kafka topics for months or years, effectively turning Kafka into a queryable, long-term storage system.[^21_3]
    * **Cost Reduction:** Dramatically lower storage costs by moving the bulk of data to cheap object storage instead of expensive, high-performance block storage (like AWS EBS).[^21_6]
    * **Simplified Backfills:** Eliminate the need for separate ETL jobs to move data from Kafka to a data lake. Applications can simply re-read historical data directly from the same topic.
    * **Faster Cluster Operations:** With less data on local broker disks, operations like broker recovery, rebalancing, and scaling become much faster.[^21_3]


#### Local vs. Remote Storage Model

Tiered Storage introduces a two-layer storage hierarchy for topic partitions :[^21_3]

1. **Local Tier (Hot Storage):** This is the traditional storage on the broker's local disks. It holds the most recent data (e.g., a few hours or days worth) and serves the majority of real-time consumer reads, benefiting from the OS page cache.[^21_1]
2. **Remote Tier (Cold/Warm Storage):** This is an external, cost-effective object store like Amazon S3, Google Cloud Storage, or HDFS.

**How it works:**

* Producers write data to the local tier as usual.[^21_5]
* As log segments on the local tier become inactive and reach a certain age or size threshold, a background process on the broker asynchronously copies them to the remote storage.[^21_5]
* Once successfully copied, the local copy of the segment can be deleted, freeing up space on the expensive local disks.[^21_1]
* The broker maintains metadata pointing to the data's location in the remote tier.[^21_5]


#### Performance Implications

* **Producers:** Unaffected. They always write to the fast, local tier.
* **Real-time Consumers:** Consumers reading recent data ("tailing the log") are also unaffected, as their data is served from the local tier's page cache.
* **Catch-up Consumers:** When a consumer requests older data that only exists in the remote tier, the request is transparently handled by the broker. The broker fetches the data from the remote object store and streams it back to the consumer. This will have **higher latency** than reading from local storage, which is the fundamental trade-off.[^21_5]
* **Kafka Version Note:** Tiered Storage was introduced as an early access feature in Apache Kafka 3.6. It is still under active development and not yet recommended for all production use cases as of early 2025. Always check the official documentation for the latest status.[^21_4]

***
Would you like to continue with the next section, "CI/CD \& DevOps"?
<span style="display:none">[^21_7]</span>

<div style="text-align: center">⁂</div>

[^21_1]: https://developers.redhat.com/articles/2024/03/13/kafka-tiered-storage-deep-dive

[^21_2]: https://www.kai-waehner.de/blog/2023/12/05/why-tiered-storage-for-apache-kafka-is-a-big-thing/

[^21_3]: https://www.uber.com/en-IN/blog/kafka-tiered-storage/

[^21_4]: https://www.instaclustr.com/blog/apache-kafka-tiered-storage-part-1/

[^21_5]: https://www.instaclustr.com/support/documentation/kafka/useful-concepts/kafka-tiered-storage/

[^21_6]: https://www.warpstream.com/blog/tiered-storage-wont-fix-kafka

[^21_7]: https://www.linkedin.com/pulse/when-kafkas-architecture-shows-its-age-innovation-happening-ranjan-qmmnc


---

# yes

Absolutely. Here is the revision guide for Section 21: CI/CD \& DevOps.

***

### 21. CI/CD \& DevOps for Kafka

Applying DevOps principles like Continuous Integration (CI) and Continuous Delivery (CD) to Kafka is crucial for managing its configuration and related applications in a reliable, repeatable, and automated way. This involves treating your Kafka resources—like topics, schemas, and ACLs—as code.[^22_3][^22_8]

#### Kafka in GitOps and CI/CD Pipelines

**GitOps** is a methodology where a Git repository serves as the single source of truth for your infrastructure's desired state. A CI/CD pipeline then automatically applies the state defined in Git to your environment.[^22_5]

* **How it works for Kafka:**

1. **Define Resources as Code:** You define Kafka topics, ACLs, schemas, and Kafka Connect configurations in declarative files (e.g., YAML or Terraform HCL) and store them in a Git repository.
2. **Pull/Merge Request:** A developer wanting to create a new topic submits a pull request with the new topic definition. This triggers a review and approval process.
3. **CI Pipeline:** On merge, a CI pipeline runs. It might lint the configuration files and run validation tests.
4. **CD Pipeline:** The CD pipeline then takes the declarative files and applies them to the Kafka cluster using appropriate tools.
* **Benefits:**
    * **Auditability:** Git history provides a complete audit trail of who changed what and when.
    * **Consistency:** Eliminates manual, error-prone changes and ensures environments (dev, staging, prod) are configured consistently.
    * **Automation:** Drastically reduces the manual effort required to manage Kafka resources.[^22_3]


#### Terraform + Helm for Infrastructure as Code

These are two popular tools for implementing Kafka as Code.

* **Terraform:** An Infrastructure as Code (IaC) tool that can manage resources across multiple cloud and service providers.
    * The **Terraform Provider for Kafka** allows you to manage topics, ACLs, and other Kafka resources declaratively.
    * **Use Case:** Ideal for managing the full lifecycle of Kafka resources alongside other cloud infrastructure (like the servers Kafka runs on).

**Real-World Example (Terraform HCL for a topic):**

```hcl
resource "kafka_topic" "orders" {
  name               = "orders-topic"
  partitions         = 12
  replication_factor = 3

  config = {
    "cleanup.policy"     = "delete"
    "retention.ms"       = "604800000" // 7 days
    "min.insync.replicas" = "2"
  }
}
```

* **Helm:** A package manager for Kubernetes.
    * If you're using Kubernetes, Helm charts can deploy Kafka (often via an Operator like Strimzi) and its related components.
    * However, Helm is primarily for application deployment, while Terraform is stronger for managing the persistent state of resources like topics.


#### Testing Kafka Configurations and Topologies

Testing is a critical part of a Kafka CI/CD pipeline.

* **Unit/Integration Testing:** For applications using Kafka (producers, consumers, Kafka Streams apps), use libraries like `spring-kafka-test` or `testcontainers`.
    * `testcontainers` can spin up a real Kafka broker in a Docker container for your tests, providing a high-fidelity testing environment without needing a shared cluster.
* **Topology Testing:** For Kafka Streams applications, the `TopologyTestDriver` allows you to test your stream processing logic without a running Kafka cluster. You can pipe records in and assert the output, making it perfect for fast unit tests.
* **Environment Parity:** Your pre-production environments (staging) should be as close to production as possible to ensure that tests are meaningful. This includes similar resource allocations, Kafka versions, and configurations.[^22_5]

***
Would you like to continue with the next section, "Real-Time Analytics"?
<span style="display:none">[^22_1][^22_2][^22_4][^22_6][^22_7][^22_9]</span>

<div style="text-align: center">⁂</div>

[^22_1]: https://www.instaclustr.com/education/apache-kafka/apache-kafka-integration-challenges-solutions-and-best-practices/

[^22_2]: https://developer.confluent.io/courses/microservices/ci-cd/

[^22_3]: https://conduktor.io/blog/kafka-gitops-for-efficient-scaling

[^22_4]: https://www.instaclustr.com/education/apache-kafka/kafka-performance-7-critical-best-practices/

[^22_5]: https://cloud.google.com/kubernetes-engine/docs/concepts/best-practices-continuous-integration-delivery-kubernetes

[^22_6]: https://www.infoq.com/articles/apache-kafka-best-practices-to-optimize-your-deployment/

[^22_7]: https://stackoverflow.com/questions/65955521/what-is-the-recommended-production-deployment-strategy-for-apache-kafka

[^22_8]: https://platformatory.io/blog/Automating-Kafka-Deployments-with-CICD/

[^22_9]: https://rjpn.org/jetnr/papers/JETNR2310003.pdf


---

# yes

Certainly. Here is the revision guide for Section 22: Real-Time Analytics.

***

### 22. Real-Time Analytics

Kafka has become the de facto standard for the data ingestion layer in modern real-time analytics pipelines. Its ability to reliably handle massive volumes of event data makes it the perfect "front door" for systems that need to process, analyze, and serve insights on data as it's created.[^23_2][^23_7]

#### Kafka + Apache Flink for Stateful Stream Processing

This is one of the most powerful combinations for real-time analytics.

* **Apache Flink:** A true stream processing framework designed for high-throughput, low-latency, and complex stateful computations on unbounded data streams.[^23_2]
* **How it works:** Flink consumes data streams directly from Kafka topics. It can perform sophisticated operations like complex event processing (CEP), windowed aggregations over event time, and joins. Flink manages its own state, with checkpoints written to durable storage (like S3), providing exactly-once processing guarantees.
* **Use Case:** Ideal for applications requiring complex logic, such as real-time fraud detection, network intrusion detection, or dynamic pricing algorithms based on live market data.


#### Kafka + Apache Spark Structured Streaming

* **Apache Spark:** A general-purpose, distributed data processing engine. Its **Structured Streaming** module processes data in a "micro-batch" model, providing a high-level, declarative API based on DataFrames and SQL.[^23_2]
* **How it works:** Spark periodically polls Kafka for new data, processes it as a small batch, and updates its results. While not a true event-at-a-time processor like Flink, its micro-batches can be as short as milliseconds, providing near-real-time performance.
* **Use Case:** A good choice for teams already familiar with the Spark ecosystem. Well-suited for ETL, data enrichment, and aggregation tasks that are less sensitive to sub-second latency.


#### Kafka + Druid / Pinot / Elasticsearch

While Flink and Spark are for *computing on streams*, these systems are **real-time analytical databases** designed for *querying streams*. They are often the "serving layer" in a real-time analytics stack.[^23_1]


| System | Description | Use Case |
| :-- | :-- | :-- |
| **Apache Druid** | A real-time analytics database purpose-built for fast slice-and-dice querying (OLAP) on large, event-oriented datasets. | Interactive dashboards and data exploration where users need to filter, group, and aggregate data with sub-second response times [^23_1]. |
| **Apache Pinot** | Similar to Druid, Pinot is a real-time distributed OLAP datastore designed for extremely high-throughput, low-latency queries. | Powering large-scale, user-facing analytical applications, such as the real-time analytics dashboard at LinkedIn [^23_5]. |
| **Elasticsearch** | A distributed search and analytics engine. It excels at full-text search, but is also widely used for log analytics and time-series data analysis. | Analyzing and searching through semi-structured log and event data, such as in a SIEM (Security Information and Event Management) system. |

**Typical Architecture:**

1. **Ingestion:** Data flows into Kafka topics from various sources.
2. **Processing (Optional):** A Kafka Streams or Flink application consumes the raw data, enriches or transforms it, and writes the results to a new "cooked" topic.
3. **Serving:** A real-time database like Druid or Pinot ingests the data from the cooked topic and makes it available for low-latency SQL queries from a dashboard or API.

***
Would you like to continue with the next section, "Disaster Recovery \& High Availability"?
<span style="display:none">[^23_3][^23_4][^23_6][^23_8]</span>

<div style="text-align: center">⁂</div>

[^23_1]: https://imply.io/whitepapers/a-data-teams-guide-to-real-time-analytics-for-apache-kafka/

[^23_2]: https://www.turing.com/resources/real-time-analytics-with-apache-kafka

[^23_3]: https://kafka.apache.org

[^23_4]: https://hevodata.com/learn/real-time-reporting-with-kafka-analytics/

[^23_5]: https://startree.ai/resources/guide-to-real-time-analytics-for-kafka/

[^23_6]: https://www.instaclustr.com/education/apache-kafka/kafka-4-use-cases-and-4-real-life-examples/

[^23_7]: https://www.qlik.com/us/streaming-data/apache-kafka

[^23_8]: https://aws.amazon.com/what-is/apache-kafka/


---

# yes

Certainly. Here is the revision guide for Section 23: Disaster Recovery \& High Availability.

***

### 23. Disaster Recovery \& High Availability

High Availability (HA) and Disaster Recovery (DR) are related but distinct concepts for ensuring business continuity.[^24_1]

* **High Availability:** Prevents service disruption from failures *within a single data center* (e.g., a single broker crash). Kafka's native replication across brokers in different racks/availability zones handles this.
* **Disaster Recovery:** Protects against the failure of an *entire data center or cloud region*. This requires replicating data to a geographically separate location.[^24_1]


#### Cross Data-Center Replication with MirrorMaker 2

The most common open-source solution for DR is to maintain a passive, standby cluster in a secondary region and use a tool to replicate data to it.[^24_3]

* **MirrorMaker 2 (MM2):** A utility that is part of the Apache Kafka project, designed to replicate topics, consumer group offsets, and topic configurations between two Kafka clusters.[^24_3]
    * **How it works:** MM2 is built on the Kafka Connect framework. It runs source connectors that consume from the primary cluster and sink connectors that produce to the secondary (standby) cluster.[^24_3]
    * **Architecture:** This is an **active-passive** DR strategy. Producers and consumers connect to the primary cluster during normal operation. In the event of a disaster, you manually fail over all clients to the secondary cluster.[^24_6]

**Key Considerations for MirrorMaker 2:**

* **Asynchronous Replication:** Replication is asynchronous, meaning there will always be some lag. This implies a non-zero **Recovery Point Objective (RPO)**; some recently committed data may be lost during a failover.[^24_7]
* **Operational Overhead:** You are responsible for running and monitoring the MM2 process and for scripting and executing the failover and failback procedures.
* **Topic Naming:** MM2 automatically renames replicated topics by prepending the source cluster's name (e.g., `primary.my-topic`). Applications must be configured to handle this change during a failover.


#### Data Backups and Snapshots

Backing up Kafka data to an external location like Amazon S3 provides an additional layer of protection, particularly against accidental data deletion or corruption (e.g., a buggy application writing poison pill messages).

* **How it works:** Use a Kafka Connect Sink connector (like the S3 Sink Connector) to continuously stream topic data to an object store.[^24_5]
* **Recovery:** Restoration involves using a source connector to read the data from S3 and write it back into a new Kafka cluster or topic. This process can be slow and is generally used for cold disaster recovery scenarios, not for rapid failover.[^24_4]


#### Partition Reassignment Tools

* `kafka-reassign-partitions.sh`: This is a crucial operational tool used for cluster maintenance and balancing. It allows you to move partition replicas from one set of brokers to another without downtime.
* **Use Cases:**
    * **Cluster Expansion:** When you add new brokers to a cluster, partitions are not automatically moved to them. You must use this tool to rebalance the cluster and spread the load.
    * **Broker Decommissioning:** Before shutting down a broker permanently, you must use this tool to move all its partition replicas to other brokers in the cluster.

***
Would you like to continue with the next section, "Kafka Client Ecosystem"?
<span style="display:none">[^24_2][^24_8][^24_9]</span>

<div style="text-align: center">⁂</div>

[^24_1]: https://www.confluent.io/resources/white-paper/best-practices-disaster-recovery/

[^24_2]: https://oso.sh/blog/building-bulletproof-disaster-recovery-for-apache-kafka-a-field-tested-architecture/

[^24_3]: https://www.warpstream.com/blog/the-hitchhikers-guide-to-disaster-recovery-and-multi-region-kafka

[^24_4]: https://aws.amazon.com/blogs/big-data/amazon-msk-replicator-and-mirrormaker2-choosing-the-right-replication-strategy-for-apache-kafka-disaster-recovery-and-migrations/

[^24_5]: https://www.confluent.io/learn/kafka-backup/

[^24_6]: https://www.youtube.com/watch?v=Gw-8gWN1zWA

[^24_7]: https://www.kai-waehner.de/blog/2025/08/04/multi-region-kafka-using-synchronous-replication-for-disaster-recovery-with-zero-data-loss-rpo0/

[^24_8]: https://www.ksolves.com/blog/big-data/apache-kafka/how-to-achieve-high-availability-for-apache-kafka

[^24_9]: https://www.instaclustr.com/education/apache-kafka/apache-kafka-architecture-a-complete-guide-2025/


---

# yes

You got it. Here is the revision guide for the final section, "Kafka Client Ecosystem".

***

### 24. Kafka Client Ecosystem

While Kafka's brokers are written in Java and Scala, its protocol is open and well-documented. This has led to a vibrant ecosystem of client libraries across many different programming languages, as well as powerful command-line tools for interaction and administration.[^25_7]

#### Official and Community Clients

The official Apache Kafka project maintains only the Java client. All other clients are developed and maintained by the community or commercial vendors like Confluent.


| Language | Popular Client(s) | Notes |
| :-- | :-- | :-- |
| **Java** | `kafka-clients` (Official) | The reference implementation. The most feature-rich and always the first to support new Kafka protocol features. The basis for frameworks like Spring Kafka. |
| **Python** | `confluent-kafka-python` | A high-performance client from Confluent that wraps the C/C++ library `librdkafka`. Generally the recommended choice for production Python applications. |
| **Python** | `kafka-python` | A pure Python client. Easier to install but generally has lower performance than the Confluent client. |
| **Go** | `confluent-kafka-go` | Similar to the Python client, this is a wrapper around `librdkafka` and is recommended for performance-critical Go applications. |
| **Go** | `sarama` | A popular, pure Go client library. Widely used and well-maintained. |
| **Node.js** | `node-rdkafka` | A high-performance client that provides a native binding to `librdkafka`. |
| **.NET** | `confluent-kafka-dotnet` | The standard C\# client, also based on `librdkafka`, for building Kafka applications on the .NET platform. |

* **`librdkafka`:** This C/C++ library is the foundation for most high-performance, non-Java clients. It is highly optimized and maintained by a key Kafka contributor, making its derivatives (like the Confluent clients for Python, Go, and .NET) very reliable and performant.


#### Kafka CLI and Confluent CLI

Command-line interface (CLI) tools are indispensable for managing and interacting with a Kafka cluster.

* **Apache Kafka CLI:** The scripts bundled with the Apache Kafka download (e.g., `kafka-topics.sh`, `kafka-console-producer.sh`, `kafka-acls.sh`).
    * **Pros:** Available with every Kafka installation.
    * **Cons:** Can be cumbersome to use, often requiring long commands with many arguments.
* **Confluent CLI:** A modern, unified command-line tool from Confluent that can manage both Confluent Cloud and on-premise Confluent Platform clusters. It provides a more user-friendly and consistent experience for managing topics, schemas, connectors, and more.
* **kcat (formerly kafkacat):** A generic, non-Java command-line producer and consumer for Kafka. It's like "netcat for Kafka" - an invaluable, lightweight tool for quick debugging, message inspection, and ad-hoc producing/consuming from the command line.

**Real-World Example (using kcat to consume from a topic):**

```bash
# Consume messages from 'my-topic' from the beginning
kcat -b localhost:9092 -t my-topic -C -o beginning
```


#### Client Configuration and Debugging

* **Configuration:** Regardless of the language, all clients are configured using the same set of key-value properties (e.g., `bootstrap.servers`, `group.id`, `acks`). The only difference is the syntax used to set them in each language.
* **Debugging:** When troubleshooting client issues, start by checking:

1. **Connectivity:** Can the client reach the `bootstrap.servers`? Firewalls and networking are the most common source of problems.
2. **Authentication/Authorization:** Is the client configured with the correct security protocol, credentials, and ACLs? Check broker logs for authentication and authorization errors.
3. **Client Logs:** Increase the client's log level to `DEBUG` to see detailed information about its internal operations, including connection attempts, fetch requests, and heartbeats.

***
You have now completed the entire quick revision guide for Apache Kafka.
<span style="display:none">[^25_1][^25_2][^25_3][^25_4][^25_5][^25_6][^25_8]</span>

<div style="text-align: center">⁂</div>

[^25_1]: https://www.instaclustr.com/education/apache-kafka/

[^25_2]: https://kafka.apache.org

[^25_3]: https://www.cloudthat.com/resources/blog/exploring-apache-kafkas-ecosystem

[^25_4]: https://learn.conduktor.io/kafka/what-is-apache-kafka/

[^25_5]: https://www.instaclustr.com/education/apache-kafka/apache-kafka-architecture-a-complete-guide-2025/

[^25_6]: https://cwiki.apache.org/confluence/display/kafka/ecosystem

[^25_7]: https://www.redpanda.com/guides/kafka-architecture-kafka-client

[^25_8]: https://learn.microsoft.com/en-us/azure/event-hubs/azure-event-hubs-apache-kafka-overview

