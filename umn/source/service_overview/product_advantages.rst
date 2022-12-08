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

      Kafka instances are compatible with Apache Kafka v1.1.0, v2.3.0, and v2.7. Keep the client and server versions the same.

-  Security

   Operations on Kafka instances are recorded and can be audited. Messages can be encrypted before storage.

   In addition to Simple Authentication and Security Layer (SASL) authentication, Virtual Private Clouds (VPCs) and security groups also provide security controls on network access.

-  Data reliability

   Kafka instances support data persistence and replication. Messages can be synchronously or asynchronously replicated between replicas and flushed to disk.

-  High availability

   Kafka runs in clusters, enabling failover and fault tolerance so that services can run smoothly.

   Kafka instance brokers can be deployed across AZs to enhance service availability.

-  Simple O&M

   The cloud service platform provides a whole set of monitoring and alarm services, eliminating the need for 24/7 attendance. Kafka instance metrics are monitored and reported, including the number of partitions, topics, and accumulated messages. You can configure alarm rules and receive SMS or email notifications on how your services are running in real time.

-  Flexible specifications

   You can customize the bandwidth and storage space for the instance and the number of partitions and replicas for topics in the instance.
