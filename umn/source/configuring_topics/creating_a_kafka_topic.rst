:original_name: kafka-ug-180604018.html

.. _kafka-ug-180604018:

Creating a Kafka Topic
======================

Topics store messages created by producers and subscribed by consumers. If **Automatic Topic Creation** is not enabled during Kafka instance creation, you need to manually create topics. If **Automatic Topic Creation** has been enabled for the instance, this operation is optional.

**Automatic Topic Creation** indicates that a topic will be automatically created when a message is produced in or consumed from a topic that does not exist. The default topic parameters are listed in :ref:`Table 1 <kafka-ug-180604018__table089295714583>`.

The following parameters of cluster instances can be changed on the **Parameters** page: **log.retention.hours** (retention period), **default.replication.factor** (replica quantity), or **num.partitions** (partition quantity). The value will be used in later topics that are automatically created.

For example, assume that **num.partitions** is changed to **5**, an automatically created topic has parameters listed in :ref:`Table 1 <kafka-ug-180604018__table089295714583>`.

.. _kafka-ug-180604018__table089295714583:

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

Methods that can be used to manually create a topic:

-  :ref:`Creating a Topic on the Console <kafka-ug-180604018__section0249155910409>`
-  :ref:`Creating a Topic on the Client <kafka-ug-180604018__section1623746152018>`

Notes and Constraints
---------------------

-  The partition quantity of topics of a single-node or cluster Kafka instance is limited. **When the partition quantity limit is reached, you can no longer create topics.** The quantity varies with instance specifications. For details, see :ref:`Cluster Kafka Instances <kafka-specification>` and :ref:`Single-node Kafka Instances <kafka-pd-0056>`.
-  For an instance with ciphertext access enabled, if **allow.everyone.if.no.acl.found** is set to **false**, topics can be created on the client only for the initial user (set when ciphertext access is enabled for the first time).
-  If a topic name starts with a special character, for example, an underscore (_) or a number sign (#), monitoring data cannot be displayed.
-  Due to the limitation of the Kafka kernel, topics whose names contain only period or underscore difference cannot be created. For example, assume that the **Topic_1** topic is created, creating a topic named **Topic.1** will fail and throw the **Topic 'topic.1' collides with existing topics: topic_1** exception.

.. _kafka-ug-180604018__section0249155910409:

Creating a Topic on the Console
-------------------------------

#. Log in to the console.

#. Click |image1| in the upper left corner to select the region where your instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click the desired Kafka instance to view the instance details.

#. In the navigation pane, choose **Topics**. Then click **Create Topic**.

#. Enter a topic name, specify other parameters, and click **OK**.


   .. figure:: /_static/images/en-us_image_0000002028172432.png
      :alt: **Figure 1** Creating a topic (cluster instance)

      **Figure 1** Creating a topic (cluster instance)

   .. table:: **Table 2** Topic parameters

      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                                                                                                                               |
      +===================================+===========================================================================================================================================================================================================================================================================================================================+
      | Topic Name                        | Customize a name that contains 3 to 200 characters, starts with a letter or underscore (_), and contains only letters, digits, periods (.), hyphens (-), and underscores (_).                                                                                                                                             |
      |                                   |                                                                                                                                                                                                                                                                                                                           |
      |                                   | The name must be different from preset topics:                                                                                                                                                                                                                                                                            |
      |                                   |                                                                                                                                                                                                                                                                                                                           |
      |                                   | -  \__consumer_offsets                                                                                                                                                                                                                                                                                                    |
      |                                   | -  \__transaction_state                                                                                                                                                                                                                                                                                                   |
      |                                   | -  \__trace                                                                                                                                                                                                                                                                                                               |
      |                                   | -  \__connect-status                                                                                                                                                                                                                                                                                                      |
      |                                   | -  \__connect-configs                                                                                                                                                                                                                                                                                                     |
      |                                   | -  \__connect-offsets                                                                                                                                                                                                                                                                                                     |
      |                                   | -  \__dms_dial_test                                                                                                                                                                                                                                                                                                       |
      |                                   |                                                                                                                                                                                                                                                                                                                           |
      |                                   | Once the topic is created, you cannot modify its name.                                                                                                                                                                                                                                                                    |
      |                                   |                                                                                                                                                                                                                                                                                                                           |
      |                                   | Due to the limitation of the Kafka kernel, topics whose names contain only period or underscore difference cannot be created. For example, assume that the **Topic_1** topic is created, creating a topic named **Topic.1** will fail and throw the **Topic 'topic.1' collides with existing topics: topic_1** exception. |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Partitions                        | Number of partitions in the topic.                                                                                                                                                                                                                                                                                        |
      |                                   |                                                                                                                                                                                                                                                                                                                           |
      |                                   | If the number of partitions is the same as that of consumers, the larger the partitions, the higher the consumption concurrency.                                                                                                                                                                                          |
      |                                   |                                                                                                                                                                                                                                                                                                                           |
      |                                   | If this parameter is set to **1**, messages will be retrieved in the FIFO order.                                                                                                                                                                                                                                          |
      |                                   |                                                                                                                                                                                                                                                                                                                           |
      |                                   | Value range: 1-200                                                                                                                                                                                                                                                                                                        |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Replicas                          | A higher number of replicas delivers higher reliability. Data is automatically backed up on each replica. When one Kafka broker becomes faulty, data is still available on other brokers.                                                                                                                                 |
      |                                   |                                                                                                                                                                                                                                                                                                                           |
      |                                   | If this parameter is set to **1**, only one set of data is available.                                                                                                                                                                                                                                                     |
      |                                   |                                                                                                                                                                                                                                                                                                                           |
      |                                   | Value range: 1 to number of brokers                                                                                                                                                                                                                                                                                       |
      |                                   |                                                                                                                                                                                                                                                                                                                           |
      |                                   | .. note::                                                                                                                                                                                                                                                                                                                 |
      |                                   |                                                                                                                                                                                                                                                                                                                           |
      |                                   |    If an instance node is faulty, an internal service error may be reported when you query messages in a topic with only one replica. Therefore, you are not advised using a topic with only one replica.                                                                                                                 |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Aging Time (h)                    | The period that messages are retained for. Consumers must retrieve messages before this period ends. Otherwise, the messages will be deleted and can no longer be consumed.                                                                                                                                               |
      |                                   |                                                                                                                                                                                                                                                                                                                           |
      |                                   | Value range: 1-720                                                                                                                                                                                                                                                                                                        |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Synchronous Replication           | A message is returned to the client only after the message creation request has been received and the message has been acknowledged by all replicas.                                                                                                                                                                      |
      |                                   |                                                                                                                                                                                                                                                                                                                           |
      |                                   | After enabling this, set the parameter **acks** to **all** or **-1** in the configuration file or production code on the producer client.                                                                                                                                                                                 |
      |                                   |                                                                                                                                                                                                                                                                                                                           |
      |                                   | If there is only one replica, synchronous replication cannot be enabled.                                                                                                                                                                                                                                                  |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Synchronous Flushing              | A message is immediately flushed to disk once it is produced, bringing higher reliability. When this option is disabled, a message is stored in the memory instead of being immediately flushed to disk once produced.                                                                                                    |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Message Timestamp                 | Timestamp type of a message. Options:                                                                                                                                                                                                                                                                                     |
      |                                   |                                                                                                                                                                                                                                                                                                                           |
      |                                   | -  **CreateTime**: time when the producer created the message.                                                                                                                                                                                                                                                            |
      |                                   | -  **LogAppendTime**: time when the broker appended the message to the log.                                                                                                                                                                                                                                               |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Max. Message Size (bytes)         | Maximum batch processing size allowed by Kafka. If message compression is enabled in the client configuration file or code of producers, this parameter indicates the size after compression.                                                                                                                             |
      |                                   |                                                                                                                                                                                                                                                                                                                           |
      |                                   | If this is increased and there are consumers older than 0.10.2, the consumers' fetch size must also be increased so that they can fetch record batches this large.                                                                                                                                                        |
      |                                   |                                                                                                                                                                                                                                                                                                                           |
      |                                   | Value range: 0 to 10,485,760                                                                                                                                                                                                                                                                                              |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   After a topic is created, view the new topic on the topic list page.

.. _kafka-ug-180604018__section1623746152018:

Creating a Topic on the Client
------------------------------

If your client is v2.2 or later, you can use **kafka-topics.sh** to create topics and manage topic parameters.

-  For a Kafka instance with ciphertext access disabled, run the following command in the **/bin** directory of the Kafka client:

   .. code-block::

      ./kafka-topics.sh --create --topic {topic-name} --bootstrap-server {connection-address} --partitions {number-of-partitions} --replication-factor {number-of-replicas}

   .. table:: **Table 3** Topic creation parameters

      +-----------------------------------+---------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                   |
      +===================================+===============================================================================================================+
      | topic-name                        | topic name, which can be customized.                                                                          |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------+
      | connection-address                | Connection address of a Kafka instance. To obtain the address, choose **Basic Information** > **Connection**. |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------+
      | number-of-partitions              | Number of partitions in the topic.                                                                            |
      |                                   |                                                                                                               |
      |                                   | To ensure performance, **200 or less** partitions are recommended for each topic.                             |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------+
      | number-of-replicas                | Number of replicas of a topic.                                                                                |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------+

   Example:

   .. code-block:: console

      [root@ecs-kafka bin]# ./kafka-topics.sh --create --topic topic-01 --bootstrap-server 192.168.xx.xx:9092,192.168.xx.xx:9092,192.168.xx.xx:9092 --partitions 3 --replication-factor 3
      Created topic topic-01.
      [root@ecs-kafka bin]#

-  For a Kafka instance with ciphertext access enabled, do as follows:

   #. (Optional) If the username and password, and the SSL certificate has been configured, skip this step and go to :ref:`2 <kafka-ug-180604018__li529219395271>`. Otherwise, do as follows:

      Create the **ssl-user-config.properties** file in the **/config** directory of the Kafka client. Add the username and password, and the SSL certificate configuration by referring to :ref:`3 <kafka-ug-180801001__li5414277457>`.

   #. .. _kafka-ug-180604018__li529219395271:

      Run the following command in the **/bin** directory of the Kafka client:

      .. code-block::

         ./kafka-topics.sh --create --topic {topic-name} --bootstrap-server {connection-address} --partitions {number-of-partitions} --replication-factor {number-of-replicas} --command-config ../config/{ssl-user-config.properties}

      .. table:: **Table 4** Topic creation parameters

         +-----------------------------------+---------------------------------------------------------------------------------------------------------------+
         | Parameter                         | Description                                                                                                   |
         +===================================+===============================================================================================================+
         | topic-name                        | topic name, which can be customized.                                                                          |
         +-----------------------------------+---------------------------------------------------------------------------------------------------------------+
         | connection-address                | Connection address of a Kafka instance. To obtain the address, choose **Basic Information** > **Connection**. |
         +-----------------------------------+---------------------------------------------------------------------------------------------------------------+
         | number-of-partitions              | Number of partitions in the topic.                                                                            |
         |                                   |                                                                                                               |
         |                                   | To ensure performance, **200 or less** partitions are recommended for each topic.                             |
         +-----------------------------------+---------------------------------------------------------------------------------------------------------------+
         | number-of-replicas                | Number of replicas of a topic.                                                                                |
         +-----------------------------------+---------------------------------------------------------------------------------------------------------------+
         | ssl-user-config.properties        | Configuration file name. This file contains username, password, and SSL certificate information.              |
         +-----------------------------------+---------------------------------------------------------------------------------------------------------------+

      Example:

      .. code-block:: console

         [root@ecs-kafka bin]# ./kafka-topics.sh --create --topic topic-01 --bootstrap-server 192.168.xx.xx:9093,192.168.xx.xx:9093,192.168.xx.xx:9093 --partitions 3 --replication-factor 3 --command-config ../config/ssl-user-config.properties
         Created topic topic-01.
         [root@ecs-kafka bin]#

.. |image1| image:: /_static/images/en-us_image_0143929918.png
