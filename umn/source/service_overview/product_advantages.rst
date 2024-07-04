:original_name: kafka-advantage.html

.. _kafka-advantage:

Product Advantages
==================

DMS provides easy-to-use message queuing based on Apache Kafka. Services can be quickly migrated to the cloud without any change, reducing maintenance and usage costs.

-  Rapid deployment

   Simply set instance information on the DMS for Kafka console, submit your order, and a complete Kafka instance will be automatically created and deployed.

-  Service migration without modifications

   DMS for Kafka is compatible with open-source Kafka APIs and supports all message processing functions of open-source Kafka.

   If your application services are developed based on open-source Kafka, you can easily migrate them to DMS after specifying a few authentication configurations.

   .. note::

      Kafka instances are compatible with Apache Kafka v1.1.0, v2.3.0, v2.7, and v3.x. Keep the client and server versions the same.

-  Security

   Operations on Kafka instances are recorded and can be audited. Messages can be encrypted before storage.

   In addition to Simple Authentication and Security Layer (SASL) authentication, Virtual Private Clouds (VPCs) and security groups also provide security controls on network access.

-  Data reliability

   Kafka instances support data persistence and replication. Messages can be synchronously or asynchronously replicated between replicas and flushed to disk.

-  High availability

   Kafka runs in clusters, enabling failover and fault tolerance so that services can run smoothly.

   Kafka instance brokers can be deployed across AZs to enhance service availability. Data is synchronized between different AZs based on Kafka's in-sync replica (ISR) mechanism. A topic must have multiple data copies and distribute them across ISRs. When ISR replication is normal, the recovery point objective (RPO) is close to 0.

-  Simple O&M

   The cloud service platform provides a whole set of monitoring and alarm services, eliminating the need for 24/7 attendance. Kafka instance metrics are monitored and reported, including the number of partitions, topics, and accumulated messages. You can configure alarm rules and receive SMS or email notifications on how your services are running in real time.

-  Massive accumulation and scaling

   Kafka features high scalability because it runs in a distributed system, or cluster. Users can configure up to 200 partitions for a topic. The storage space, broker quantity and flavor can be also expanded. This means that billions of messages can be accumulated, suitable for scenarios requiring high concurrency, high performance, and large-scale access.

-  Flexible specifications

   You can customize the bandwidth and storage space for the instance and the number of partitions and replicas for topics in the instance.
