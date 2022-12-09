:original_name: Kafka-specification.html

.. _Kafka-specification:

Specifications
==============

Kafka Instance Specifications
-----------------------------

Kafka instances are compatible with open-source Kafka 1.1.0, 2.3.0, and 2.7. The instance specifications are classified based on bandwidth, namely, 100 MB/s, 300 MB/s, 600 MB/s, and 1200 MB/s.

.. _kafka-specification__en-us_topic_0159429488_table78751014154818:

.. table:: **Table 1** TPS and the maximum number of partitions supported by different instance specifications and I/O types

   +-----------+----------------+-----------------------+-------------------------------+--------------------+
   | Bandwidth | I/O Type       | TPS (High-Throughput) | TPS (Synchronous Replication) | Maximum Partitions |
   +===========+================+=======================+===============================+====================+
   | 100 MB/s  | High I/O       | 100,000               | 60,000                        | 300                |
   +-----------+----------------+-----------------------+-------------------------------+--------------------+
   |           | Ultra-high I/O | 100,000               | 80,000                        | 300                |
   +-----------+----------------+-----------------------+-------------------------------+--------------------+
   | 300 MB/s  | High I/O       | 300,000               | 150,000                       | 900                |
   +-----------+----------------+-----------------------+-------------------------------+--------------------+
   |           | Ultra-high I/O | 300,000               | 200,000                       | 900                |
   +-----------+----------------+-----------------------+-------------------------------+--------------------+
   | 600 MB/s  | Ultra-high I/O | 600,000               | 300,000                       | 1800               |
   +-----------+----------------+-----------------------+-------------------------------+--------------------+
   | 1200 MB/s | Ultra-high I/O | 1,200,000             | 400,000                       | 1800               |
   +-----------+----------------+-----------------------+-------------------------------+--------------------+

.. note::

   For Kafka instances, the number of transactions per second (TPS) is the maximum number of messages that can be written per second. The preceding TPS is calculated with each message being 1 KB.

Bandwidth Selection
-------------------

The bandwidth of a Kafka instance refers to the maximum read or write bandwidth. You are advised to select a bandwidth 30% higher than what is required.

-  100 MB/s

   Recommended for up to 3000 client connections, 60 consumer groups, and 70 MB/s service traffic.

-  300 MB/s

   Recommended for up to 10,000 client connections, 300 consumer groups, and 210 MB/s service traffic.

-  600 MB/s

   Recommended for up to 20,000 client connections, 600 consumer groups, and 420 MB/s service traffic.

-  1200 MB/s

   Recommended for up to 20,000 client connections, 600 consumer groups, and 840 MB/s service traffic.

Storage Space Selection
-----------------------

Kafka instances support storage with 1 to 3 replicas. The storage space is consumed by all replicas. When creating an instance, specify its storage space based on the expected service message size and the number of replicas.

For example, if the estimated message size is 100 GB, the disk capacity must be at least: 100 GB x Number of replicas + 100 GB (reserved space).

Topic Quantity
--------------

There are limits on the topic quantity and the aggregate number of partitions in the topics. When the partition quantity limit is reached, you can no longer create topics.

The number of topics is related to the maximum number of partitions allowed and the specified number of partitions in each topic (see :ref:`Table 1 <kafka-specification__en-us_topic_0159429488_table78751014154818>`).

**The maximum number of partitions for a 100 MB/s instance is 300.**

-  If the number of partitions of each topic in the instance is 3, the maximum number of topics is 300/3 = 100.
-  If the number of partitions of each topic in the instance is 1, the maximum number of topics is 300/1 = 300.
