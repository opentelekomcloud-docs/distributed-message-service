:original_name: kafka-ug-0038.html

.. _kafka-ug-0038:

Modifying Kafka Topic Configurations
====================================

This section describes how to modify configurations in :ref:`Table 1 <kafka-ug-0038__table19803102744620>` of a Kafka topic on the console.

Modifying **Synchronous Replication**, **Synchronous Flushing**, **Message Timestamp**, or **Max. Message Size** does not require instance restart.

.. _kafka-ug-0038__table19803102744620:

.. table:: **Table 1** Kafka topic configuration parameters

   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter                         | Description                                                                                                                                                            |
   +===================================+========================================================================================================================================================================+
   | Partitions                        | Number of partitions in a topic. For details about how to change, see :ref:`Changing Kafka Partition Quantity <kafka-ug-0006>`.                                        |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Aging Time (h)                    | Maximum message retention. For details about how to change, see :ref:`Changing Kafka Message Retention Period <kafka-ug-200506001>`.                                   |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Replicas                          | Number of replicas of each topic partition. To modify it, see :ref:`Modifying Kafka Topic Replicas <kafka-ug-0072>`.                                                   |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Synchronous Replication           | A message is returned to the client only after the message creation request has been received and the message has been acknowledged by all replicas.                   |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Synchronous Flushing              | -  Enabled: A message is immediately flushed to disk once it is created, bringing higher reliability.                                                                  |
   |                                   | -  Disabled: A message is stored in the memory instead of being immediately flushed to disk once created.                                                              |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Message Timestamp                 | Timestamp type of a message. Options:                                                                                                                                  |
   |                                   |                                                                                                                                                                        |
   |                                   | -  **CreateTime**: time when the producer created the message.                                                                                                         |
   |                                   | -  **LogAppendTime**: time when the broker appended the message to the log.                                                                                            |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Max. Message Size                 | Maximum size of messages to be processed in batches. If message compression is enabled, this parameter indicates the size after compression.                           |
   |                                   |                                                                                                                                                                        |
   |                                   | If this value is increased and the consumer version is earlier than 0.10.2, the consumers' fetch size must also be increased so that they can obtain the latest value. |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Notes and Constraints
---------------------

-  If there is only one replica, **Synchronous Replication** cannot be enabled.
-  After enabling synchronous replication, set **acks** to **all** or **-1** on the client. Otherwise, this function will not take effect.

Modifying a Topic
-----------------

#. Log in to the console.

#. Click |image1| in the upper left corner to select the region where your instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click the desired instance to go to the instance details page.

#. In the navigation pane, choose **Topics**.

#. Modify topic configurations in either of the following ways:

   -  Select one or more topics and click **Edit Topic** above the topic list.
   -  In the row containing the desired topic, click **Edit**.

#. In the **Edit Topic** dialog box, change configurations and click **OK**.

   View the reconfiguration on the **Topics** page.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
