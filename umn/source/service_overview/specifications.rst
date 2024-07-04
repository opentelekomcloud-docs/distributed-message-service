:original_name: Kafka-specification.html

.. _Kafka-specification:

Specifications
==============

Kafka Instance Specifications
-----------------------------

Kafka instances are compatible with open-source Kafka v1.1.0, v2.3.0, v2.7, and v3.x. Kafka instances are classified into cluster and single-node types. A cluster instance consists of three or more brokers and a single-node one has one broker.

Kafka instances are classified based on instance ECS flavors as follows:

-  Cluster

   -  kafka.2u4g.cluster.small
   -  kafka.2u4g.cluster
   -  kafka.4u8g.cluster
   -  kafka.8u16g.cluster
   -  kafka.12u24g.cluster
   -  kafka.16u32g.cluster
   -  kafka.2u4g.cluster.beta
   -  kafka.4u8g.cluster.beta

-  Single-node

   -  kafka.2u4g.single.small
   -  kafka.2u4g.single

.. note::

   For Kafka instances, the number of transactions per second (TPS) is the maximum number of messages that can be written per second. In the following table, transactions per second (TPS) are calculated assuming that the size of a message is 1 KB. The test scenario is private access in plaintext. The disk type is ultra-high I/O.

   Cluster Kafka instances support v1.1.0, v2.3.0, v2.7, and v3.x. Single-node Kafka instances support v2.7.

.. _kafka-specification__table152020206204:

.. table:: **Table 1** Kafka instance specifications (v1.1.0/v2.3.0/v2.7 cluster instances)

   +--------------------------+---------+------------------------+-------------------------------+----------------------------------------+---------------------------------------+---------------------+---------------------------+
   | Flavor                   | Brokers | Maximum TPS per Broker | Maximum Partitions per Broker | Recommended Consumer Groups per Broker | Maximum Client Connections per Broker | Storage Space       | Traffic per Broker (MB/s) |
   +==========================+=========+========================+===============================+========================================+=======================================+=====================+===========================+
   | kafka.2u4g.cluster.small | 3-30    | 20,000                 | 100                           | 15                                     | 2000                                  | 300 GB-300,000 GB   | 40                        |
   +--------------------------+---------+------------------------+-------------------------------+----------------------------------------+---------------------------------------+---------------------+---------------------------+
   | kafka.2u4g.cluster       | 3-30    | 30,000                 | 250                           | 20                                     | 2000                                  | 300 GB-300,000 GB   | 100                       |
   +--------------------------+---------+------------------------+-------------------------------+----------------------------------------+---------------------------------------+---------------------+---------------------------+
   | kafka.4u8g.cluster       | 3-30    | 100,000                | 500                           | 100                                    | 4000                                  | 300 GB-600,000 GB   | 200                       |
   +--------------------------+---------+------------------------+-------------------------------+----------------------------------------+---------------------------------------+---------------------+---------------------------+
   | kafka.8u16g.cluster      | 3-50    | 150,000                | 1000                          | 150                                    | 4000                                  | 300 GB-1,500,000 GB | 250                       |
   +--------------------------+---------+------------------------+-------------------------------+----------------------------------------+---------------------------------------+---------------------+---------------------------+
   | kafka.12u24g.cluster     | 3-50    | 200,000                | 1500                          | 200                                    | 4000                                  | 300 GB-1,500,000 GB | 375                       |
   +--------------------------+---------+------------------------+-------------------------------+----------------------------------------+---------------------------------------+---------------------+---------------------------+
   | kafka.16u32g.cluster     | 3-50    | 250,000                | 2000                          | 200                                    | 4000                                  | 300 GB-1,500,000 GB | 500                       |
   +--------------------------+---------+------------------------+-------------------------------+----------------------------------------+---------------------------------------+---------------------+---------------------------+

.. table:: **Table 2** Kafka instance specifications (v3.x cluster instances)

   +-------------------------+---------+----------------+-------------------------------+----------------------------------------+---------------------------------------+---------------+---------------------------+
   | Flavor                  | Brokers | TPS per Broker | Maximum Partitions per Broker | Recommended Consumer Groups per Broker | Maximum Client Connections per Broker | Storage Space | Traffic per Broker (MB/s) |
   +=========================+=========+================+===============================+========================================+=======================================+===============+===========================+
   | kafka.2u4g.cluster.beta | 3       | 30,000         | 250                           | 20                                     | 2000                                  | 300 GB        | 100                       |
   +-------------------------+---------+----------------+-------------------------------+----------------------------------------+---------------------------------------+---------------+---------------------------+
   | kafka.4u8g.cluster.beta | 3       | 100,000        | 500                           | 100                                    | 4000                                  | 300 GB        | 200                       |
   +-------------------------+---------+----------------+-------------------------------+----------------------------------------+---------------------------------------+---------------+---------------------------+

.. _kafka-specification__table960115533719:

.. table:: **Table 3** Kafka instance specifications (single-node)

   +-------------------------+---------+----------------+-------------------------------+----------------------------------------+---------------------------------------+------------------+---------------------------+
   | Flavor                  | Brokers | TPS per Broker | Maximum Partitions per Broker | Recommended Consumer Groups per Broker | Maximum Client Connections per Broker | Storage Space    | Traffic per Broker (MB/s) |
   +=========================+=========+================+===============================+========================================+=======================================+==================+===========================+
   | kafka.2u4g.single.small | 1       | 20,000         | 100                           | 15                                     | 2000                                  | 100 GB-10,000 GB | 40                        |
   +-------------------------+---------+----------------+-------------------------------+----------------------------------------+---------------------------------------+------------------+---------------------------+
   | kafka.2u4g.single       | 1       | 30,000         | 250                           | 20                                     | 2000                                  | 100 GB-10,000 GB | 100                       |
   +-------------------------+---------+----------------+-------------------------------+----------------------------------------+---------------------------------------+------------------+---------------------------+

Instance Specifications and Network Bandwidth
---------------------------------------------

The network bandwidth of a Kafka instance consists of the following:

#. Network bandwidth used by the instance brokers
#. Bandwidth of the disk used by the instance brokers. For details, see `Disk Types and Performance <https://docs.otc.t-systems.com/en-us/usermanual/evs/en-us_topic_0014580744.html>`__.

Note:

-  By default, Kafka tests are performed in the tail read scenario (that is, only the latest production data is consumed) instead of the cold read scenario (that is, historical data is consumed from the beginning).
-  The bandwidth of an instance with an old flavor (such as 100 MB/s) is the total network bandwidth of the instance's all brokers.

**Traffic calculation of instances with new flavors (such as kafka.2u4g.cluster) is described as follows:**

-  The read/write ratio is 1:1.
-  The default number of topic replicas is 3.
-  Total network traffic = Traffic per broker x Broker quantity
-  Total instance traffic = Service traffic + Data replication traffic between brokers

Assume that the current flavor is kafka.2u4g.cluster, the traffic per broker is 100 MB/s, and the number of brokers is 3. What are the total network traffic, maximum read traffic, and maximum write traffic of the instance?

#. Total network traffic = Traffic per broker x Broker quantity = 100 MB/s x 3 = 300 MB/s
#. Maximum read traffic = Total instance network traffic/Default number of replicas/2 = 300 MB/s/3/2= 50 MB/s
#. Maximum write traffic = Total instance network traffic/Default number of replicas/2 = 300 MB/s/3/2 = 50 MB/s

Mapping Between Old and New Flavors
-----------------------------------

:ref:`Table 4 <kafka-specification__table16919145814010>` compares the old and new Kafka instance flavors.

.. _kafka-specification__table16919145814010:

.. table:: **Table 4** Mapping between old and new Kafka instance flavors

   +------------+--------------------------------+-------------------------------+--------------------------------+
   | Old Flavor |                                | New Flavor                    |                                |
   +============+================================+===============================+================================+
   | Flavor     | Total Instance Network Traffic | Flavor                        | Total Instance Network Traffic |
   +------------+--------------------------------+-------------------------------+--------------------------------+
   | 100 MB/s   | 100 MB/s                       | kafka.2u4g.cluster.small \* 3 | 120 MB/s                       |
   +------------+--------------------------------+-------------------------------+--------------------------------+
   | 300 MB/s   | 300 MB/s                       | kafka.2u4g.cluster \* 3       | 300 MB/s                       |
   +------------+--------------------------------+-------------------------------+--------------------------------+
   | 600 MB/s   | 600 MB/s                       | kafka.4u8g.cluster \* 3       | 600 MB/s                       |
   +------------+--------------------------------+-------------------------------+--------------------------------+
   | 1200 MB/s  | 1200 MB/s                      | kafka.4u8g.cluster \* 6       | 1250 MB/s                      |
   +------------+--------------------------------+-------------------------------+--------------------------------+

Instances with new flavors have the following features:

-  Better performance and cost effectiveness: They use exclusive resources (except for kafka.2u4g.cluster.small). By contrast, old flavors use non-exclusive resources. If the load is heavy, resources conflicts will occur.
-  Latest functions, for example, reassigning partitions and changing the SSL setting.
-  Flexible flavor changes: For example, you can increase the broker flavor.
-  Flexible disk capacity: Only related to the broker quantity, and not to the flavor.
-  More specification options: A wider range of combinations of broker flavor (over 10,000 MB/s) and quantity are available.

Flavor Selection
----------------

-  kafka.2u4g.cluster.small with 3 brokers

   Recommended for up to 6000 client connections, 45 consumer groups, and 60,000 TPS

-  kafka.2u4g.cluster with 3 brokers

   Recommended for up to 6000 client connections, 60 consumer groups, and 90,000 TPS

-  kafka.4u8g.cluster with 3 brokers

   Recommended for up to 12,000 client connections, 300 consumer groups, and 300,000 TPS

-  kafka.8u16g.cluster with 3 brokers

   Recommended for up to 12,000 client connections, 450 consumer groups, and 450,000 TPS

-  kafka.12u24g.cluster with 3 brokers

   Recommended for up to 12,000 client connections, 600 consumer groups, and 600,000 TPS

-  kafka.16u32g.cluster with 3 brokers

   Recommended for up to 12,000 client connections, 600 consumer groups, and 750,000 TPS

Storage Space Selection
-----------------------

Kafka instances can store messages in multiple replicas. The storage space is consumed by message replicas, logs, and metadata. When creating an instance, specify its storage space based on the expected service message size, the number of replicas, and reserved disk space. Each Kafka broker reserves 33 GB disk space for storing logs and metadata.

For example, if the expected service message size is 100 GB, the number of replicas is 2, and the number of brokers is 3, the disk size should be at least 299 GB (100 GB x 2 + 33 GB x 3).

The storage space can be expanded as your service grows.

Topic Quantity
--------------

There are limits on the topic quantity and the aggregate number of partitions in the topics. When the partition quantity limit is reached, you can no longer create topics.

The number of topics is related to the maximum number of partitions allowed (see :ref:`Figure 1 <kafka-specification__fig1391435820518>`) and the specified number of partitions in each topic (see :ref:`Table 1 <kafka-specification__table152020206204>` and :ref:`Table 3 <kafka-specification__table960115533719>`).

.. _kafka-specification__fig1391435820518:

.. figure:: /_static/images/en-us_image_0000001755301270.png
   :alt: **Figure 1** Setting the number of partitions

   **Figure 1** Setting the number of partitions

**The maximum number of partitions allowed for an instance with kafka.2u4g.cluster and 3 brokers is 750.**

-  If the number of partitions of each topic in the instance is 3, the maximum number of topics is 750/3 = 250.
-  If the number of partitions of each topic in the instance is 1, the maximum number of topics is 750/1 = 750.
