:original_name: glossary-kafka.html

.. _glossary-kafka:

Basic Concepts
==============

DMS for Kafka of the cloud service platform uses Kafka as the message engine. This chapter presents explanations of basic concepts of Kafka.

Topic
-----

A topic is a category for messages. Messages are created, retrieved, and managed in the form of topics.

Topics adopt the publish-subscribe pattern. Producers publish messages into topics. One or more consumers subscribe to the messages in the topics. The producers and consumers are not directly linked to each other.

Producer
--------

A producer publishes messages into topics. The messages are then delivered to other systems or modules for processing as agreed.

Consumer
--------

A consumer subscribes to messages in topics and processes the messages. For example, a monitoring and alarm platform (a consumer) subscribing to log messages in certain topics can identify alarm logs and then send SMS or email alarm notifications.

Broker
------

A broker is a Kafka process in a Kafka cluster. Each process runs on a server, so a broker includes the storage, bandwidth, and other server resources.

Partition
---------

A topic is divided into partitions. Messages are distributed to multiple partitions to achieve scalability and fault tolerance.

Replica
-------

A replica is a redundant copy of a partition in a topic. Each partition can have one or more replicas, enabling message reliability.

Messages in each partition are fully replicated and synchronized, preventing data loss if one replica fails.

Each partition has one replica as the leader which handles the creation and retrievals of all messages. The rest replicas are followers which replicate the leader.

Topics and partitions are logical concepts, while replicas and brokers are physical concepts. The following diagram shows the relationships between partitions, brokers, and topics in messages streaming.


.. figure:: /_static/images/en-us_image_0169395994.png
   :alt: **Figure 1** Kafka message streaming

   **Figure 1** Kafka message streaming

Aging Time
----------

The period that messages are retained for. Consumers must retrieve messages before this period ends. Otherwise, the messages will be deleted and can no longer be retrieved.
