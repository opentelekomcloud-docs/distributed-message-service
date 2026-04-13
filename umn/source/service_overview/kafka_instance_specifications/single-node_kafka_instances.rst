:original_name: kafka-pd-0056.html

.. _kafka-pd-0056:

Single-node Kafka Instances
===========================

Instance Specifications
-----------------------

A single-node Kafka instance has one broker, is compatible with open-source Kafka 2.7, and is applicable to test scenarios. Do not use it for production services.

.. note::

   In the following table:

   -  For Kafka instances, the number of **transactions per second (TPS)** is the maximum number of messages that can be written per second.
   -  **TPS performance**: number of messages processed per second assuming that the size of a message is 1 KB.
   -  **Test scenario**: private access in plaintext. The disk type is ultra-high I/O.

.. _kafka-pd-0056__table960115533719:

.. table:: **Table 1** Single-node Kafka instance specifications

   +-------------------------+---------+---------------------+----------------------------+----------------------------------------+------------------------------------+--------------------+---------------------------------+
   | Flavor                  | Brokers | Max. TPS per Broker | Max. Partitions per Broker | Recommended Consumer Groups per Broker | Max. Client Connections per Broker | Storage Space (GB) | Traffic Limit per Broker (MB/s) |
   +=========================+=========+=====================+============================+========================================+====================================+====================+=================================+
   | kafka.2u4g.single.small | 1       | 20,000              | 100                        | 15                                     | 2,000                              | 100-10,000         | 40                              |
   +-------------------------+---------+---------------------+----------------------------+----------------------------------------+------------------------------------+--------------------+---------------------------------+
   | kafka.2u4g.single       | 1       | 30,000              | 250                        | 20                                     | 2,000                              | 100-10,000         | 100                             |
   +-------------------------+---------+---------------------+----------------------------+----------------------------------------+------------------------------------+--------------------+---------------------------------+

Storage Space Estimation
------------------------

Kafka instances can store messages in multiple replicas. The storage space is consumed by message replicas, logs, and metadata. When creating an instance, specify its storage space based on the expected service message size, the number of replicas, and reserved disk space. Each Kafka broker reserves 33 GB disk space for storing logs and metadata.

For example, if the expected service message size is 100 GB, the number of replicas is 2, and the number of brokers is 1, the disk size should be at least 233 GB (100 GB x 2 + 33 GB x 1).

Topic Quantity Calculation
--------------------------

There are limits on the topic quantity and the aggregate number of partitions in the topics. When the partition quantity limit is reached, you can no longer create topics.

The number of topics is related to the maximum number of partitions allowed and the specified number of partitions in each topic (see :ref:`Table 1 <kafka-pd-0056__table960115533719>`).

**The maximum number of partitions allowed for an instance with kafka.2u4g.single is 250.**

-  If the number of partitions of each topic in the instance is 2, the maximum number of topics is 250/2 = 125.
-  If the number of partitions of each topic in the instance is 1, the maximum number of topics is 250/1 = 250.
