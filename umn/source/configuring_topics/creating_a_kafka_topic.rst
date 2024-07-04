:original_name: kafka-ug-180604018.html

.. _kafka-ug-180604018:

Creating a Kafka Topic
======================

Topics store messages created by producers and subscribed by consumers. If automatic topic creation is not enabled during Kafka instance creation, you need to manually create topics. If automatic topic creation has been enabled for the instance, this operation is optional.

Automatic topic creation: A topic will be automatically created when a message is produced in or consumed from a topic that does not exist. By default, the topic has parameters listed in :ref:`Table 1 <kafka-ug-180604018__table7806193043818>`.

After you change the value of the **log.retention.hours**, **default.replication.factor**, or **num.partitions** parameter, the value will be used in later topics that are automatically created. For example, assume that **num.partitions** is changed to 5, an automatically created topic has parameters listed in :ref:`Table 1 <kafka-ug-180604018__table7806193043818>`.

.. _kafka-ug-180604018__table7806193043818:

.. table:: **Table 1** Topic parameters

   ========================= ============= ==============
   Parameter                 Default Value Modified Value
   ========================= ============= ==============
   Partitions                3             5
   Replicas                  3             3
   Aging Time (h)            72            72
   Synchronous Replication   Disabled      Disabled
   Synchronous Flushing      Disabled      Disabled
   Message Timestamp         CreateTime    CreateTime
   Max. Message Size (bytes) 10,485,760    10,485,760
   ========================= ============= ==============

Methods that can be used to manually create a topic:

-  :ref:`Method 1: Creating a Topic on the Console <kafka-ug-180604018__section0249155910409>`
-  :ref:`Method 2: Creating a Topic by Using Kafka CLI <kafka-ug-180604018__section1623746152018>`

Constraints
-----------

-  The total number of partitions in topics is limited. **When the partition quantity limit is reached, you can no longer create topics.** The total number of partitions varies by instance specifications. For details, see :ref:`Specifications <kafka-specification>`.
-  If an instance node is faulty, an internal service error may be reported when you query messages in a topic with only one replica. Therefore, you are not advised using a topic with only one replica.

.. _kafka-ug-180604018__section0249155910409:

Method 1: Creating a Topic on the Console
-----------------------------------------

#. Log in to the console.

#. Click |image1| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click the desired Kafka instance to view the instance details.

#. In the navigation pane, choose **Topics**. Then click **Create Topic**.


   .. figure:: /_static/images/en-us_image_0000001803876329.png
      :alt: **Figure 1** Creating a topic

      **Figure 1** Creating a topic

#. Specify the topic parameters listed in the following table.

   .. table:: **Table 2** Topic parameters

      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                               |
      +===================================+===========================================================================================================================================================================================================+
      | Topic Name                        | Customize a name that contains 3 to 200 characters, starts with a letter or underscore (_), and contains only letters, digits, periods (.), hyphens (-), and underscores (_).                             |
      |                                   |                                                                                                                                                                                                           |
      |                                   | The name must be different from preset topics:                                                                                                                                                            |
      |                                   |                                                                                                                                                                                                           |
      |                                   | -  \_consumer_offsets                                                                                                                                                                                     |
      |                                   | -  \_transaction_state                                                                                                                                                                                    |
      |                                   | -  \_trace                                                                                                                                                                                                |
      |                                   | -  \_connect-status                                                                                                                                                                                       |
      |                                   | -  \_connect-configs                                                                                                                                                                                      |
      |                                   | -  \_connect-offsets                                                                                                                                                                                      |
      |                                   |                                                                                                                                                                                                           |
      |                                   | Once the topic is created, you cannot modify its name.                                                                                                                                                    |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Partitions                        | Number of partitions in the topic.                                                                                                                                                                        |
      |                                   |                                                                                                                                                                                                           |
      |                                   | If the number of partitions is the same as that of consumers, the larger the partitions, the higher the consumption concurrency.                                                                          |
      |                                   |                                                                                                                                                                                                           |
      |                                   | If this parameter is set to **1**, messages will be retrieved in the FIFO order.                                                                                                                          |
      |                                   |                                                                                                                                                                                                           |
      |                                   | Value range: 1 to 200                                                                                                                                                                                     |
      |                                   |                                                                                                                                                                                                           |
      |                                   | Default value: **3**                                                                                                                                                                                      |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Replicas                          | A higher number of replicas delivers higher reliability. Data is automatically backed up on each replica. When one Kafka broker becomes faulty, data is still available on other brokers.                 |
      |                                   |                                                                                                                                                                                                           |
      |                                   | If this parameter is set to **1**, only one set of data is available.                                                                                                                                     |
      |                                   |                                                                                                                                                                                                           |
      |                                   | Value range: 1 to number of brokers                                                                                                                                                                       |
      |                                   |                                                                                                                                                                                                           |
      |                                   | .. note::                                                                                                                                                                                                 |
      |                                   |                                                                                                                                                                                                           |
      |                                   |    If an instance node is faulty, an internal service error may be reported when you query messages in a topic with only one replica. Therefore, you are not advised using a topic with only one replica. |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Aging Time (h)                    | The period that messages are retained for. Consumers must retrieve messages before this period ends. Otherwise, the messages will be deleted and can no longer be consumed.                               |
      |                                   |                                                                                                                                                                                                           |
      |                                   | Value range: 1-720                                                                                                                                                                                        |
      |                                   |                                                                                                                                                                                                           |
      |                                   | Default value: **72**                                                                                                                                                                                     |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Synchronous Replication           | A message is returned to the client only after the message creation request has been received and the message has been acknowledged by all replicas.                                                      |
      |                                   |                                                                                                                                                                                                           |
      |                                   | After enabling this, set the parameter **acks** to **all** or **-1** in the configuration file or production code on the producer client.                                                                 |
      |                                   |                                                                                                                                                                                                           |
      |                                   | If there is only one replica, synchronous replication cannot be enabled.                                                                                                                                  |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Synchronous Flushing              | -  Enabled: A message is immediately flushed to disk once it is created, bringing higher reliability.                                                                                                     |
      |                                   | -  Disabled: A message is stored in the memory instead of being immediately flushed to disk once created.                                                                                                 |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Message Timestamp                 | Timestamp type of a message. Options:                                                                                                                                                                     |
      |                                   |                                                                                                                                                                                                           |
      |                                   | -  **CreateTime**: time when the producer created the message.                                                                                                                                            |
      |                                   | -  **LogAppendTime**: time when the broker appended the message to the log.                                                                                                                               |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Max. Message Size                 | Maximum batch processing size allowed by Kafka. If message compression is enabled in the client configuration file or code of producers, this parameter indicates the size after compression.             |
      |                                   |                                                                                                                                                                                                           |
      |                                   | If this is increased and there are consumers older than 0.10.2, the consumers' fetch size must also be increased so that they can fetch record batches this large.                                        |
      |                                   |                                                                                                                                                                                                           |
      |                                   | Value range: 0 to 10,485,760                                                                                                                                                                              |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Click **OK**.

.. _kafka-ug-180604018__section1623746152018:

Method 2: Creating a Topic by Using Kafka CLI
---------------------------------------------

If your client is v2.2 or later, you can use **kafka-topics.sh** to create topics and manage topic parameters.

.. important::

   -  If a topic name starts with a special character, for example, an underscore (_) or a number sign (#), monitoring data cannot be displayed.
   -  For an instance with ciphertext access enabled, if **allow.everyone.if.no.acl.found** is set to **false**, topics cannot be created through the client.

-  For a Kafka instance with ciphertext access disabled, run the following command in the **/bin** directory of the Kafka client:

   .. code-block::

      ./kafka-topics.sh --create --topic ${topic-name} --bootstrap-server ${connection-address} --partitions ${number-of-partitions} --replication-factor ${number-of-replicas}

-  For a Kafka instance with ciphertext access enabled, do as follows:

   #. (Optional) For the Kafka security protocol, is SASL_PLAINTEXT or SASL_SSL used?

      -  SASL_PLAINTEXT: Skip this step if the username and password are already set. In other cases, create the **ssl-user-config.properties** file in the **/config** directory of the Kafka client. Add the username and password by referring to :ref:`3 <kafka-ug-180801001__li5414277457>`.
      -  SASL_SSL: Skip this step if the username, password, and SSL certificate are already set. In other cases, create the **ssl-user-config.properties** file in the **/config** directory of the Kafka client. Add the username and password, and the SSL certificate configuration by referring to :ref:`3 <kafka-ug-180801001__li5414277457>`.

   #. Run the following command in the **/bin** directory of the Kafka client:

      .. code-block::

         ./kafka-topics.sh --create --topic ${topic-name} --bootstrap-server ${connection-address} --partitions ${number-of-partitions} --replication-factor ${number-of-replicas} --command-config ./config/ssl-user-config.properties

.. |image1| image:: /_static/images/en-us_image_0143929918.png
