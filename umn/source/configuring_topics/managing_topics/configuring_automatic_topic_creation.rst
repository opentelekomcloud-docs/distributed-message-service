:original_name: kafka_ug_0043.html

.. _kafka_ug_0043:

Configuring Automatic Topic Creation
====================================

**Automatic Topic Creation** indicates that a topic will be automatically created when a message is produced in or consumed from a topic that does not exist. By default, the topic has parameters listed in :ref:`Table 1 <kafka_ug_0043__table512723410377>`.

The following parameters of cluster instances can be changed on the **Parameters** page: **log.retention.hours** (retention period), **default.replication.factor** (replica quantity), or **num.partitions** (partition quantity). The value will be used in later topics that are automatically created.

For example, assume that **num.partitions** is changed to **5**, an automatically created topic has parameters listed in :ref:`Table 1 <kafka_ug_0043__table512723410377>`.

.. _kafka_ug_0043__table512723410377:

.. table:: **Table 1** Topic parameters

   +---------------------------+-----------------------------+-------------------------+-----------------------+
   | Parameter                 | Default Value (Single-node) | Default Value (Cluster) | Modified To (Cluster) |
   +===========================+=============================+=========================+=======================+
   | Partitions                | 1                           | 3                       | 5                     |
   +---------------------------+-----------------------------+-------------------------+-----------------------+
   | Replicas                  | 1                           | 3                       | 3                     |
   +---------------------------+-----------------------------+-------------------------+-----------------------+
   | Aging Time (h)            | 72                          | 72                      | 72                    |
   +---------------------------+-----------------------------+-------------------------+-----------------------+
   | Synchronous Replication   | Disabled                    | Disabled                | Disabled              |
   +---------------------------+-----------------------------+-------------------------+-----------------------+
   | Synchronous Flushing      | Disabled                    | Disabled                | Disabled              |
   +---------------------------+-----------------------------+-------------------------+-----------------------+
   | Message Timestamp         | CreateTime                  | CreateTime              | CreateTime            |
   +---------------------------+-----------------------------+-------------------------+-----------------------+
   | Max. Message Size (bytes) | 10,485,760                  | 10,485,760              | 10,485,760            |
   +---------------------------+-----------------------------+-------------------------+-----------------------+

Notes and Constraints
---------------------

Enabling or disabling automatic topic creation may restart the instance.

Procedure
---------

#. Log in to the console.
#. Click |image1| in the upper left corner to select the region where your instance is located.
#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.
#. Click the name of the desired Kafka instance to go to the **Basic Information** page.
#. In the **Instance Information** area, click |image2| or |image3| next to **Automatic Topic Creation**. The **Confirm** dialog box is displayed.
#. Click **OK**. The **Background Tasks** page is displayed. Automatic topic creation has been configured when the task is in the **Successful** state.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
.. |image2| image:: /_static/images/en-us_image_0000001283221910.png
.. |image3| image:: /_static/images/en-us_image_0000001191767177.png
