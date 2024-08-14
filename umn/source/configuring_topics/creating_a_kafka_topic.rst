:original_name: kafka-ug-180604018.html

.. _kafka-ug-180604018:

Creating a Kafka Topic
======================

Topics store messages created by producers and subscribed by consumers. If **Automatic Topic Creation** is not enabled during Kafka instance creation, you need to manually create topics. If **Automatic Topic Creation** has been enabled for the instance, this operation is optional.

**Automatic Topic Creation** indicates that a topic will be automatically created when a message is produced in or consumed from a topic that does not exist. The default topic parameters are listed in :ref:`Table 1 <kafka-ug-180604018__table7806193043818>`.

After you change the value of the **log.retention.hours** (retention period), **default.replication.factor** (replica quantity), or **num.partitions** (partition quantity) parameter, the value will be used in later topics that are automatically created. For example, assume that **num.partitions** is changed to 5, an automatically created topic has parameters listed in :ref:`Table 1 <kafka-ug-180604018__table7806193043818>`.

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

-  :ref:`Creating a Topic (Console) <kafka-ug-180604018__section0249155910409>`
-  :ref:`Creating a Topic (Client) <kafka-ug-180604018__section1623746152018>`

Constraints
-----------

-  The total number of partitions in topics is limited. **When the partition quantity limit is reached, you can no longer create topics.** The total number of partitions varies by instance specifications. For details, see :ref:`Specifications <kafka-specification>`.
-  If an instance node is faulty, an internal service error may be reported when you query messages in a topic with only one replica. Therefore, you are not advised using a topic with only one replica.

.. _kafka-ug-180604018__section0249155910409:

Creating a Topic (Console)
--------------------------

#. Log in to the console.

#. Click |image1| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click the desired Kafka instance to view the instance details.

#. In the navigation pane, choose **Topics**. Then click **Create Topic**.

#. Enter a topic name, specify other parameters, and click **OK**.


   .. figure:: /_static/images/en-us_image_0000001992720829.png
      :alt: **Figure 1** Creating a topic

      **Figure 1** Creating a topic

   .. table:: **Table 2** Topic parameters

      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                            |
      +===================================+========================================================================================================================================================================================================================+
      | Topic Name                        | Customize a name that contains 3 to 200 characters, starts with a letter or underscore (_), and contains only letters, digits, periods (.), hyphens (-), and underscores (_).                                          |
      |                                   |                                                                                                                                                                                                                        |
      |                                   | The name must be different from preset topics:                                                                                                                                                                         |
      |                                   |                                                                                                                                                                                                                        |
      |                                   | -  \__consumer_offsets                                                                                                                                                                                                 |
      |                                   | -  \__transaction_state                                                                                                                                                                                                |
      |                                   | -  \__trace                                                                                                                                                                                                            |
      |                                   | -  \__connect-status                                                                                                                                                                                                   |
      |                                   | -  \__connect-configs                                                                                                                                                                                                  |
      |                                   | -  \__connect-offsets                                                                                                                                                                                                  |
      |                                   |                                                                                                                                                                                                                        |
      |                                   | Once the topic is created, you cannot modify its name.                                                                                                                                                                 |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Partitions                        | Number of partitions in the topic.                                                                                                                                                                                     |
      |                                   |                                                                                                                                                                                                                        |
      |                                   | If the number of partitions is the same as that of consumers, the larger the partitions, the higher the consumption concurrency.                                                                                       |
      |                                   |                                                                                                                                                                                                                        |
      |                                   | If this parameter is set to **1**, messages will be retrieved in the FIFO order.                                                                                                                                       |
      |                                   |                                                                                                                                                                                                                        |
      |                                   | Value range: 1 to 200                                                                                                                                                                                                  |
      |                                   |                                                                                                                                                                                                                        |
      |                                   | Default value: **3**                                                                                                                                                                                                   |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Replicas                          | A higher number of replicas delivers higher reliability. Data is automatically backed up on each replica. When one Kafka broker becomes faulty, data is still available on other brokers.                              |
      |                                   |                                                                                                                                                                                                                        |
      |                                   | If this parameter is set to **1**, only one set of data is available.                                                                                                                                                  |
      |                                   |                                                                                                                                                                                                                        |
      |                                   | Value range: 1 to number of brokers                                                                                                                                                                                    |
      |                                   |                                                                                                                                                                                                                        |
      |                                   | .. note::                                                                                                                                                                                                              |
      |                                   |                                                                                                                                                                                                                        |
      |                                   |    If an instance node is faulty, an internal service error may be reported when you query messages in a topic with only one replica. Therefore, you are not advised using a topic with only one replica.              |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Aging Time (h)                    | The period that messages are retained for. Consumers must retrieve messages before this period ends. Otherwise, the messages will be deleted and can no longer be consumed.                                            |
      |                                   |                                                                                                                                                                                                                        |
      |                                   | Value range: 1-720                                                                                                                                                                                                     |
      |                                   |                                                                                                                                                                                                                        |
      |                                   | Default value: **72**                                                                                                                                                                                                  |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Synchronous Replication           | A message is returned to the client only after the message creation request has been received and the message has been acknowledged by all replicas.                                                                   |
      |                                   |                                                                                                                                                                                                                        |
      |                                   | After enabling this, set the parameter **acks** to **all** or **-1** in the configuration file or production code on the producer client.                                                                              |
      |                                   |                                                                                                                                                                                                                        |
      |                                   | If there is only one replica, synchronous replication cannot be enabled.                                                                                                                                               |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Synchronous Flushing              | A message is immediately flushed to disk once it is produced, bringing higher reliability. When this option is disabled, a message is stored in the memory instead of being immediately flushed to disk once produced. |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Message Timestamp                 | Timestamp type of a message. Options:                                                                                                                                                                                  |
      |                                   |                                                                                                                                                                                                                        |
      |                                   | -  **CreateTime**: time when the producer created the message.                                                                                                                                                         |
      |                                   | -  **LogAppendTime**: time when the broker appended the message to the log.                                                                                                                                            |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Max. Message Size                 | Maximum batch processing size allowed by Kafka. If message compression is enabled in the client configuration file or code of producers, this parameter indicates the size after compression.                          |
      |                                   |                                                                                                                                                                                                                        |
      |                                   | If this is increased and there are consumers older than 0.10.2, the consumers' fetch size must also be increased so that they can fetch record batches this large.                                                     |
      |                                   |                                                                                                                                                                                                                        |
      |                                   | Value range: 0 to 10,485,760                                                                                                                                                                                           |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _kafka-ug-180604018__section1623746152018:

Creating a Topic (Client)
-------------------------

If your client is v2.2 or later, you can use **kafka-topics.sh** to create topics and manage topic parameters.

.. important::

   -  If a topic name starts with a special character, for example, an underscore (_) or a number sign (#), monitoring data cannot be displayed.
   -  For an instance with ciphertext access enabled, if **allow.everyone.if.no.acl.found** is set to **false**, topics cannot be created through the client.

-  For a Kafka instance with ciphertext access disabled, run the following command in the **/bin** directory of the Kafka client:

   .. code-block::

      ./kafka-topics.sh --create --topic ${topic-name} --bootstrap-server ${connection-address} --partitions ${number-of-partitions} --replication-factor ${number-of-replicas}

   Parameter description:

   -  **topic-name**: topic name, which can be customized.
   -  **connection-address**: can be obtained from the **Connection** area on the **Basic Information** page on the Kafka console.
   -  **number-of-partitions**: number of partitions in a topic.
   -  **number-of-replicas**: number of replicas in a topic.

   Example:

   .. code-block:: console

      [root@ecs-kafka bin]# ./kafka-topics.sh --create --topic topic-01 --bootstrap-server 192.168.xx.xx:9092,192.168.xx.xx:9092,192.168.xx.xx:9092 --partitions 3 --replication-factor 3
      Created topic topic-01.
      [root@ecs-kafka bin]#

-  For a Kafka instance with ciphertext access enabled, do as follows:

   #. (Optional) Modify the client configuration file.

      View **Security Protocol** in the **Connection** area on the **Basic Information** page on the Kafka console. The configuration settings vary depending on the protocol.

      -  SASL_PLAINTEXT: Skip this step if the username and password are already set. Otherwise, create the **ssl-user-config.properties** file in the **/config** directory on the Kafka client and add the following content to the file:

         .. code-block::

            security.protocol=SASL_PLAINTEXT
            # If the SASL mechanism is SCRAM-SHA-512, configure as follows:
            sasl.jaas.config=org.apache.kafka.common.security.scram.ScramLoginModule required \
            username="**********" \
            password="**********";
            sasl.mechanism=SCRAM-SHA-512
            # If the SASL mechanism is PLAIN, configure as follows:
            sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required \
            username="**********" \
            password="**********";
            sasl.mechanism=PLAIN

         Parameter description: **username** and **password** are the ones you set when enabling ciphertext access for the first time or when creating a user.

      -  SASL_SSL: Skip this step if the username, password, and SSL certificate are already set. Otherwise, create the **ssl-user-config.properties** file in the **/config** directory on the Kafka client and add the following content to the file:

         .. code-block::

            security.protocol=SASL_SSL
            ssl.truststore.location={ssl_truststore_path}
            ssl.truststore.password=dms@kafka
            ssl.endpoint.identification.algorithm=
            # If the SASL mechanism is SCRAM-SHA-512, configure as follows:
            sasl.jaas.config=org.apache.kafka.common.security.scram.ScramLoginModule required \
            username="**********" \
            password="**********";
            sasl.mechanism=SCRAM-SHA-512
            # If the SASL mechanism is PLAIN, configure as follows:
            sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required \
            username="**********" \
            password="**********";
            sasl.mechanism=PLAIN

         Parameter description:

         -  **ssl.truststore.location**: path for storing the **client.jks** certificate. Even in Windows, you need to use slashes (/) for the certificate path. Do not use backslashes (\\), which are used by default for paths in Windows. Otherwise, the client will fail to obtain the certificate.
         -  **ssl.truststore.password**: server certificate password, which must be set to **dms@kafka** and cannot be changed.
         -  **ssl.endpoint.identification.algorithm**: whether to verify the certificate domain name. **This parameter must be left blank, which indicates disabling domain name verification**.
         -  **username** and **password**: username and password you set when enabling ciphertext access for the first time or when creating a user.

   #. Run the following command in the **/bin** directory of the Kafka client:

      .. code-block::

         ./kafka-topics.sh --create --topic ${topic-name} --bootstrap-server ${connection-address} --partitions ${number-of-partitions} --replication-factor ${number-of-replicas} --command-config ../config/ssl-user-config.properties

      Parameter description:

      -  **topic-name**: topic name, which can be customized.
      -  **connection-address**: can be obtained from the **Connection** area on the **Basic Information** page on the Kafka console.
      -  **number-of-partitions**: number of partitions in a topic.
      -  **number-of-replicas**: number of replicas in a topic.

      Example:

      .. code-block:: console

         [root@ecs-kafka bin]# ./kafka-topics.sh --create --topic topic-01 --bootstrap-server 192.168.xx.xx:9093,192.168.xx.xx:9093,192.168.xx.xx:9093 --partitions 3 --replication-factor 3 --command-config ../config/ssl-user-config.properties
         Created topic topic-01.
         [root@ecs-kafka bin]#

.. |image1| image:: /_static/images/en-us_image_0143929918.png
