:original_name: kafka-ug-0038.html

.. _kafka-ug-0038:

Modifying Kafka Topic Configurations
====================================

This section describes how to modify following configurations of a Kafka topic on the console.

.. note::

   Modifying **Synchronous Replication**, **Synchronous Flushing**, **Message Timestamp**, or **Max. Message Size** does not require instance restart.

.. table:: **Table 1** Kafka topic configuration parameters

   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter                         | Description                                                                                                                                                            |
   +===================================+========================================================================================================================================================================+
   | Partitions                        | Number of partitions in a topic. For details about how to change, see :ref:`Changing Kafka Partition Quantity <kafka-ug-0006>`.                                        |
   +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Aging Time (h)                    | Maximum message retention. For details about how to change, see :ref:`Changing Kafka Message Retention Period <kafka-ug-200506001>`.                                   |
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

Procedure
---------

#. Log in to the console.
#. Click |image1| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.
#. Click the desired Kafka instance to view the instance details.
#. In the navigation pane, choose **Topics**.
#. Modify topic configurations in either of the following ways:

   -  Select one or more topics and click **Edit Topic** above the topic list.
   -  In the row containing the desired topic, click **Edit**.

#. In the **Edit Topic** dialog box, change configurations and click **OK**.

   .. note::

      -  If there is only one replica, **Synchronous Replication** cannot be enabled.
      -  After enabling synchronous replication, set **acks** to **all** or **-1** on the client. Otherwise, this function will not take effect.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
