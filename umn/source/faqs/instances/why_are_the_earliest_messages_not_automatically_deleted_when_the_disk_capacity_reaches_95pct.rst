:original_name: kafka-faq-0070.html

.. _kafka-faq-0070:

Why Are the Earliest Messages Not Automatically Deleted When the Disk Capacity Reaches 95%?
===========================================================================================

Symptom
-------

Each broker of a Kafka instance has a 100 GB disk. The automatic deletion policy has been configured and a topic with 180 partitions has been created. The earliest messages are not automatically deleted when the disk usage reaches 95%.

Possible Cause
--------------

Each broker of a Kafka instance uses a 33 GB disk to store logs and ZooKeeper data. Such a disk was formatted during instance creation and certain space is used. As a result, the data storage space is approximately 66 GB. Several segment files constitute each partition of a topic. Each segment file has maximum storage of 500 MB. To delete a message, Kafka deletes segment files instead of a message. Kafka reserves at least one segment file in each partition for message storage. In this way, at least one segment file is kept. Increasing partitions to 132 (66 GB/500 MB = 132) may cause the disk usage to reach the upper limit.

When the disk usage reaches 95% (62.7 GB), the messages might be stored in one of those kept segment files. In this case, the messages are not deleted.

Solution
--------

Expand the storage. For details, see :ref:`Modifying Cluster Kafka Instance Specifications <kafka-ug-181221001>`
