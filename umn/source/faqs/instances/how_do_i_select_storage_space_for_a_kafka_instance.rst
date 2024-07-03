:original_name: kafka-faq-200426005.html

.. _kafka-faq-200426005:

How Do I Select Storage Space for a Kafka Instance?
===================================================

The storage space is the space for storing messages (including messages in replicas), logs and metadata. To select a storage space, specify the disk type and disk size. For more information, see `Disk Types and Performance <https://docs.otc.t-systems.com/en-us/usermanual/evs/en-us_topic_0014580744.html>`__.

For example, if the required disk size to store data for the retention period is 100 GB, the disk capacity must be at least: **100 GB x Number of replicas + 100 GB (reserved space)**. In a Kafka cluster, each node uses a 33 GB disk to store logs and ZooKeeper data. Therefore, the actual available storage space is less than the created storage space.

The number of replicas (3 by default) can be configured when you create a topic. If automatic topic creation has been enabled, each automatically created topic has three replicas by default. You can change this quantity by setting **default.replication.factor** on the **Parameters** tab page.
