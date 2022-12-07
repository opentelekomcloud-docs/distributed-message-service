:original_name: dms-ug-180604018.html

.. _dms-ug-180604018:

Creating a Topic
================

A topic is a stream of messages. If automatic topic creation is not enabled during Kafka instance creation, you need to manually create topics for creating and retrieving messages. If automatic topic creation has been enabled for the instance, this operation is optional.

If automatic topic creation is enabled, the system automatically creates a topic when a message is created in or retrieved from a topic that does not exist. This topic has the following default settings: 3 partitions, 3 replicas, aging time 72 hours, and synchronous replication and flushing disabled. After you change the value of the **log.retention.hours**, **default.replication.factor**, or **num.partitions** parameter, automatically created topics later use the new value. For example, if **num.partitions** is set to 5, an automatically created topic will have the following settings: 5 partitions, 3 replicas, aging time 72 hours, and synchronous replication and flushing disabled.

There is a limit on the total number of partitions in topics. **When the partition quantity limit is reached, you can no longer create topics.** The total number of partitions varies with instance specifications. For details, see :ref:`Specifications <kafka-specification>`.

Methods that can be used to manually create a topic:

-  :ref:`Method 1: Creating a Topic on the Console <dms-ug-180604018__section0249155910409>`
-  :ref:`Method 2: Create a Topic by Using Kafka CLI <dms-ug-180604018__section1623746152018>`

.. note::

   If an instance node is faulty, an internal service error may be reported when you query messages in a topic with only one replica. Therefore, you are not advised to use a topic with only one replica.

.. _dms-ug-180604018__section0249155910409:

Method 1: Creating a Topic on the Console
-----------------------------------------

#. Log in to the management console.

#. Click |image1| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click the desired Kafka instance to view the instance details.

#. Click the **Topics** tab, and click **Create Topic**.

   The **Create Topic** dialog box is displayed.

#. Specify the topic parameters listed in the following table.

   .. table:: **Table 1** Topic parameters

      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                |
      +===================================+============================================================================================================================================================================================================+
      | Topic Name                        | When creating a topic, you can modify the automatically generated topic name.                                                                                                                              |
      |                                   |                                                                                                                                                                                                            |
      |                                   | Once the topic is created, you cannot modify its name.                                                                                                                                                     |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Partitions                        | A larger number of partitions for a topic indicates more messages retrieved concurrently.                                                                                                                  |
      |                                   |                                                                                                                                                                                                            |
      |                                   | If this parameter is set to **1**, messages will be retrieved in the FIFO order.                                                                                                                           |
      |                                   |                                                                                                                                                                                                            |
      |                                   | Value range: 1 to 100                                                                                                                                                                                      |
      |                                   |                                                                                                                                                                                                            |
      |                                   | Default value: **3**                                                                                                                                                                                       |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Replicas                          | A higher number of replicas delivers higher reliability. Data is automatically backed up on each replica. When one Kafka broker becomes faulty, data is still available on other brokers.                  |
      |                                   |                                                                                                                                                                                                            |
      |                                   | If this parameter is set to **1**, only one set of data is available.                                                                                                                                      |
      |                                   |                                                                                                                                                                                                            |
      |                                   | Value range: 1 to 3                                                                                                                                                                                        |
      |                                   |                                                                                                                                                                                                            |
      |                                   | Default value: **3**                                                                                                                                                                                       |
      |                                   |                                                                                                                                                                                                            |
      |                                   | .. note::                                                                                                                                                                                                  |
      |                                   |                                                                                                                                                                                                            |
      |                                   |    If an instance node is faulty, an internal service error may be reported when you query messages in a topic with only one replica. Therefore, you are not advised to use a topic with only one replica. |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Aging Time (h)                    | The period that messages are retained for. Consumers must retrieve messages before this period ends. Otherwise, the messages will be deleted and can no longer be retrieved.                               |
      |                                   |                                                                                                                                                                                                            |
      |                                   | Value range: 1 to 720                                                                                                                                                                                      |
      |                                   |                                                                                                                                                                                                            |
      |                                   | Default value: **72**                                                                                                                                                                                      |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Synchronous Replication           | A message is returned to the client only after the message creation request has been received and the message has been acknowledged by all replicas.                                                       |
      |                                   |                                                                                                                                                                                                            |
      |                                   | After enabling synchronous replication, set **acks** to **all** or **-1** on the client. Otherwise, this function will not take effect.                                                                    |
      |                                   |                                                                                                                                                                                                            |
      |                                   | If there is only one replica, synchronous replication cannot be enabled.                                                                                                                                   |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Synchronous Flushing              | An indicator of whether a message is immediately flushed to disk once created.                                                                                                                             |
      |                                   |                                                                                                                                                                                                            |
      |                                   | -  Enabled: A message is immediately flushed to disk once it is created, resulting in higher reliability.                                                                                                  |
      |                                   | -  Disabled: A message is stored in the memory instead of being immediately flushed to disk once created.                                                                                                  |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Click **OK**.

.. _dms-ug-180604018__section1623746152018:

Method 2: Create a Topic by Using Kafka CLI
-------------------------------------------

If your client is v2.2 or later, you can use **kafka-topics.sh** to create topics and manage topic parameters.

.. important::

   If a topic name starts with a special character, for example, an underscore (_) or a number sign (#), monitoring data cannot be displayed.

-  If SASL is not enabled for the Kafka instance, run the following command in the **/**\ *{directory where the CLI is located}*\ **/kafka_{version}/bin/** directory to create a topic:

   .. code-block::

      ./kafka-topics.sh --create --topic {topic_name} --bootstrap-server {broker_ip}:{port} --partitions {partition_num} --replication-factor {replication_num}

-  If SASL has been enabled for the Kafka instance, perform the following steps to create a topic:

   #. (Optional) If the SSL certificate configuration has been set, skip this step. Otherwise, perform the following operations:

      Create the **ssl-user-config.properties** file in the **/config** directory of the Kafka client and add the SSL certificate configurations by referring to :ref:`3 <kafka-ug-180801001__li5414277457>`.

   #. Run the following command in the **/**\ *{directory where the CLI is located}*\ **/kafka_{version}/bin/** directory to create a topic:

      .. code-block::

         ./kafka-topics.sh --create --topic {topic_name} --bootstrap-server {broker_ip}:{port} --partitions {partition_num} --replication-factor {replication_num} --command-config ./config/ssl-user-config.properties

.. |image1| image:: /_static/images/en-us_image_0143929918.png
