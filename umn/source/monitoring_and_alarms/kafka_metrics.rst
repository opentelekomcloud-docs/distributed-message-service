:original_name: kafka-ug-180413002.html

.. _kafka-ug-180413002:

Kafka Metrics
=============

Introduction
------------

This section describes metrics reported by DMS to Cloud Eye as well as their namespaces and dimensions. You can use the Cloud Eye console or APIs to query the Kafka metrics and alarms, or view Kafka instance metrics on the **Monitoring** page of the DMS console.

For example, you can call the `API <https://docs.otc.t-systems.com/en-us/api/ces/ces_03_0033.html>`__ to query the monitoring data of the **Disk Capacity Usage** metric.

Namespace
---------

SYS.DMS

Instance Metrics
----------------

.. table:: **Table 1** Instance metrics

   +--------------------+----------------------+-----------------------------------------------------------------------------+-----------------+-------+-----------------+------------------------------+------------------------------+
   | Metric ID          | Metric Name          | Description                                                                 | Value Range     | Unit  | Conversion Rule | Monitored Object (Dimension) | Monitoring Period (Raw Data) |
   +====================+======================+=============================================================================+=================+=======+=================+==============================+==============================+
   | current_partitions | Partitions           | Number of used partitions in the instance                                   | 0-100,000       | Count | N/A             | Kafka instance               | 1 minute                     |
   +--------------------+----------------------+-----------------------------------------------------------------------------+-----------------+-------+-----------------+------------------------------+------------------------------+
   | current_topics     | Topics               | Number of created topics in the instance                                    | 0-100,000       | Count | N/A             | Kafka instance               | 1 minute                     |
   +--------------------+----------------------+-----------------------------------------------------------------------------+-----------------+-------+-----------------+------------------------------+------------------------------+
   | group_msgs         | Accumulated Messages | Total number of accumulated messages in all consumer groups of the instance | 0-1,000,000,000 | Count | N/A             | Kafka instance               | 1 minute                     |
   +--------------------+----------------------+-----------------------------------------------------------------------------+-----------------+-------+-----------------+------------------------------+------------------------------+

Broker Metrics
--------------

Enabling Smart Connect for a Kafka instance creates two or more brokers. On the **By Broker** tab page, select "connector" for **Node Type** for Smart Connect broker metrics, or select "broker" for **Node Type** for Kafka instance broker metrics.

Metrics of Smart Connect brokers: disk capacity usage, memory usage, JVM heap memory usage, node alive status, and connections.

.. table:: **Table 2** Broker metrics

   +------------------------------+-----------------------------------------------+------------------------------------------------------------------------------+---------------------+---------+-----------------+------------------------------+------------------------------+
   | Metric ID                    | Metric Name                                   | Description                                                                  | Value Range         | Unit    | Conversion Rule | Monitored Object (Dimension) | Monitoring Period (Raw Data) |
   +==============================+===============================================+==============================================================================+=====================+=========+=================+==============================+==============================+
   | broker_data_size             | Message Size                                  | Total size of messages in the broker                                         | 0-5,000,000,000,000 | Byte    | 1024(IEC)       | Kafka instance broker        | 1 minute                     |
   +------------------------------+-----------------------------------------------+------------------------------------------------------------------------------+---------------------+---------+-----------------+------------------------------+------------------------------+
   | broker_messages_in_rate      | Message Creation Rate                         | Number of messages created per second                                        | 0-500,000           | Count/s | N/A             | Kafka instance broker        | 1 minute                     |
   +------------------------------+-----------------------------------------------+------------------------------------------------------------------------------+---------------------+---------+-----------------+------------------------------+------------------------------+
   | broker_bytes_out_rate        | Message Retrieval                             | Number of bytes retrieved per second                                         | 0-500,000,000       | Byte/s  | 1024(IEC)       | Kafka instance broker        | 1 minute                     |
   +------------------------------+-----------------------------------------------+------------------------------------------------------------------------------+---------------------+---------+-----------------+------------------------------+------------------------------+
   | broker_bytes_in_rate         | Message Creation                              | Number of bytes created per second                                           | 0-500,000,000       | Byte/s  | 1024(IEC)       | Kafka instance broker        | 1 minute                     |
   +------------------------------+-----------------------------------------------+------------------------------------------------------------------------------+---------------------+---------+-----------------+------------------------------+------------------------------+
   | broker_public_bytes_in_rate  | Public Inbound Traffic                        | Inbound traffic over public networks per second                              | 0-500,000,000       | Byte/s  | 1024(IEC)       | Kafka instance broker        | 1 minute                     |
   |                              |                                               |                                                                              |                     |         |                 |                              |                              |
   |                              |                                               | You can view this metric if public access has been enabled for the instance. |                     |         |                 |                              |                              |
   +------------------------------+-----------------------------------------------+------------------------------------------------------------------------------+---------------------+---------+-----------------+------------------------------+------------------------------+
   | broker_public_bytes_out_rate | Public Outbound Traffic                       | Outbound traffic over public networks per second                             | 0-500,000,000       | Byte/s  | 1024(IEC)       | Kafka instance broker        | 1 minute                     |
   |                              |                                               |                                                                              |                     |         |                 |                              |                              |
   |                              |                                               | You can view this metric if public access has been enabled for the instance. |                     |         |                 |                              |                              |
   +------------------------------+-----------------------------------------------+------------------------------------------------------------------------------+---------------------+---------+-----------------+------------------------------+------------------------------+
   | broker_fetch_mean            | Average Message Retrieval Processing Duration | Average time that the broker spends processing message retrieval requests    | 0-10,000            | ms      | N/A             | Kafka instance broker        | 1 minute                     |
   +------------------------------+-----------------------------------------------+------------------------------------------------------------------------------+---------------------+---------+-----------------+------------------------------+------------------------------+
   | broker_produce_mean          | Average Message Creation Processing Duration  | Average time that the broker spends processing message creation requests     | 0-10,000            | ms      | N/A             | Kafka instance broker        | 1 minute                     |
   +------------------------------+-----------------------------------------------+------------------------------------------------------------------------------+---------------------+---------+-----------------+------------------------------+------------------------------+
   | broker_cpu_core_load         | Average Load per CPU Core                     | Average load of each CPU core of the Kafka VM                                | 0-20                | N/A     | N/A             | Kafka instance broker        | 1 minute                     |
   +------------------------------+-----------------------------------------------+------------------------------------------------------------------------------+---------------------+---------+-----------------+------------------------------+------------------------------+
   | broker_disk_usage            | Disk Capacity Usage                           | Disk usage of the Kafka VM                                                   | 0-100               | %       | N/A             | Kafka instance broker        | 1 minute                     |
   +------------------------------+-----------------------------------------------+------------------------------------------------------------------------------+---------------------+---------+-----------------+------------------------------+------------------------------+
   | broker_memory_usage          | Memory Usage                                  | Memory usage of the Kafka VM                                                 | 0-100               | %       | N/A             | Kafka instance broker        | 1 minute                     |
   +------------------------------+-----------------------------------------------+------------------------------------------------------------------------------+---------------------+---------+-----------------+------------------------------+------------------------------+
   | broker_heap_usage            | JVM Heap Memory Usage of JVM                  | Heap memory usage of the Kafka JVM                                           | 0-100               | %       | N/A             | Kafka instance broker        | 1 minute                     |
   +------------------------------+-----------------------------------------------+------------------------------------------------------------------------------+---------------------+---------+-----------------+------------------------------+------------------------------+
   | broker_alive                 | Broker Alive                                  | Whether the Kafka broker is alive                                            | -  **1**: alive     | N/A     | N/A             | Kafka instance broker        | 1 minute                     |
   |                              |                                               |                                                                              | -  **0**: not alive |         |                 |                              |                              |
   +------------------------------+-----------------------------------------------+------------------------------------------------------------------------------+---------------------+---------+-----------------+------------------------------+------------------------------+
   | broker_connections           | Connections                                   | Total number of TCP connections on the Kafka broker                          | 0-65,535            | Count   | N/A             | Kafka instance broker        | 1 minute                     |
   +------------------------------+-----------------------------------------------+------------------------------------------------------------------------------+---------------------+---------+-----------------+------------------------------+------------------------------+
   | broker_cpu_usage             | CPU Usage                                     | CPU usage of the Kafka VM                                                    | 0-100               | %       | N/A             | Kafka instance broker        | 1 minute                     |
   +------------------------------+-----------------------------------------------+------------------------------------------------------------------------------+---------------------+---------+-----------------+------------------------------+------------------------------+
   | broker_disk_read_await       | Average Disk Read Time                        | Average time for each disk I/O read in the monitoring period                 | > 0                 | ms      | N/A             | Kafka instance broker        | 1 minute                     |
   +------------------------------+-----------------------------------------------+------------------------------------------------------------------------------+---------------------+---------+-----------------+------------------------------+------------------------------+
   | broker_disk_write_await      | Average Disk Write Time                       | Average time for each disk I/O write in the monitoring period                | > 0                 | ms      | N/A             | Kafka instance broker        | 1 minute                     |
   +------------------------------+-----------------------------------------------+------------------------------------------------------------------------------+---------------------+---------+-----------------+------------------------------+------------------------------+
   | broker_total_bytes_in_rate   | Inbound Traffic                               | Inbound traffic per second                                                   | 0-1,000,000,000     | Byte/s  | 1024(IEC)       | Kafka instance broker        | 1 minute                     |
   +------------------------------+-----------------------------------------------+------------------------------------------------------------------------------+---------------------+---------+-----------------+------------------------------+------------------------------+
   | broker_total_bytes_out_rate  | Outbound Traffic                              | Outbound traffic per second                                                  | 0-1,000,000,000     | Byte/s  | 1024(IEC)       | Kafka instance broker        | 1 minute                     |
   +------------------------------+-----------------------------------------------+------------------------------------------------------------------------------+---------------------+---------+-----------------+------------------------------+------------------------------+
   | broker_disk_read_rate        | Disk Read Speed                               | Read traffic on the disk                                                     | >= 0                | Byte/s  | 1024(IEC)       | Kafka instance broker        | 1 minute                     |
   +------------------------------+-----------------------------------------------+------------------------------------------------------------------------------+---------------------+---------+-----------------+------------------------------+------------------------------+
   | broker_disk_write_rate       | Disk Write Speed                              | Write traffic on the disk                                                    | >= 0                | Byte/s  | 1024(IEC)       | Kafka instance broker        | 1 minute                     |
   +------------------------------+-----------------------------------------------+------------------------------------------------------------------------------+---------------------+---------+-----------------+------------------------------+------------------------------+

Topic Metrics
-------------

.. table:: **Table 3** Topic metrics

   +------------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------+---------------------+---------+-----------------+------------------------------+------------------------------+
   | Metric ID              | Metric Name           | Description                                                                                                             | Value Range         | Unit    | Conversion Rule | Monitored Object (Dimension) | Monitoring Period (Raw Data) |
   +========================+=======================+=========================================================================================================================+=====================+=========+=================+==============================+==============================+
   | topic_bytes_in_rate    | Message Creation      | Number of bytes created per second                                                                                      | 0-500,000,000       | Byte/s  | 1024(IEC)       | Topic in a Kafka instance    | 1 minute                     |
   |                        |                       |                                                                                                                         |                     |         |                 |                              |                              |
   |                        |                       | This metric is available only when **Monitoring Type** is set to **Basic monitoring** on the **By Topic** tab page.     |                     |         |                 |                              |                              |
   +------------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------+---------------------+---------+-----------------+------------------------------+------------------------------+
   | topic_bytes_out_rate   | Message Retrieval     | Number of bytes retrieved per second                                                                                    | 0-500,000,000       | Byte/s  | 1024(IEC)       | Topic in a Kafka instance    | 1 minute                     |
   |                        |                       |                                                                                                                         |                     |         |                 |                              |                              |
   |                        |                       | This metric is available only when **Monitoring Type** is set to **Basic monitoring** on the **By Topic** tab page.     |                     |         |                 |                              |                              |
   +------------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------+---------------------+---------+-----------------+------------------------------+------------------------------+
   | topic_data_size        | Message Size          | Total size of messages in the queue                                                                                     | 0-5,000,000,000,000 | Byte    | 1024(IEC)       | Topic in a Kafka instance    | 1 minute                     |
   |                        |                       |                                                                                                                         |                     |         |                 |                              |                              |
   |                        |                       | This metric is available only when **Monitoring Type** is set to **Basic monitoring** on the **By Topic** tab page.     |                     |         |                 |                              |                              |
   +------------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------+---------------------+---------+-----------------+------------------------------+------------------------------+
   | topic_messages         | Total Messages        | Total number of messages in the queue                                                                                   | >= 0                | Count   | N/A             | Topic in a Kafka instance    | 1 minute                     |
   |                        |                       |                                                                                                                         |                     |         |                 |                              |                              |
   |                        |                       | This metric is available only when **Monitoring Type** is set to **Basic monitoring** on the **By Topic** tab page.     |                     |         |                 |                              |                              |
   +------------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------+---------------------+---------+-----------------+------------------------------+------------------------------+
   | topic_messages_in_rate | Message Creation Rate | Number of messages created per second                                                                                   | 0-500,000           | Count/s | N/A             | Topic in a Kafka instance    | 1 minute                     |
   |                        |                       |                                                                                                                         |                     |         |                 |                              |                              |
   |                        |                       | This metric is available only when **Monitoring Type** is set to **Basic monitoring** on the **By Topic** tab page.     |                     |         |                 |                              |                              |
   +------------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------+---------------------+---------+-----------------+------------------------------+------------------------------+
   | partition_messages     | Partition Messages    | Total number of messages in the partition                                                                               | >= 0                | Count   | N/A             | Topic in a Kafka instance    | 1 minute                     |
   |                        |                       |                                                                                                                         |                     |         |                 |                              |                              |
   |                        |                       | This metric is available only when **Monitoring Type** is set to **Partition monitoring** on the **By Topic** tab page. |                     |         |                 |                              |                              |
   +------------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------+---------------------+---------+-----------------+------------------------------+------------------------------+
   | produced_messages      | Created Messages      | Number of messages that have been created                                                                               | >= 0                | Count   | N/A             | Topic in a Kafka instance    | 1 minute                     |
   |                        |                       |                                                                                                                         |                     |         |                 |                              |                              |
   |                        |                       | This metric is available only when **Monitoring Type** is set to **Partition monitoring** on the **By Topic** tab page. |                     |         |                 |                              |                              |
   +------------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------+---------------------+---------+-----------------+------------------------------+------------------------------+

Consumer Group Metrics
----------------------

.. table:: **Table 4** Consumer group metrics

   +----------------------------+-----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------+--------+-----------------+------------------------------------+------------------------------+
   | Metric ID                  | Metric Name                 | Description                                                                                                                                                                    | Value Range         | Unit   | Conversion Rule | Monitored Object (Dimension)       | Monitoring Period (Raw Data) |
   +============================+=============================+================================================================================================================================================================================+=====================+========+=================+====================================+==============================+
   | messages_consumed          | Retrieved Messages          | Number of messages that have been retrieved in the consumer group                                                                                                              | >= 0                | Count  | N/A             | Consumer group of a Kafka instance | 1 minute                     |
   |                            |                             |                                                                                                                                                                                |                     |        |                 |                                    |                              |
   |                            |                             | This metric is available only when **Topic** is set to a specific topic name and **Monitoring Type** is set to **Partition monitoring** on the **By Consumer Group** tab page. |                     |        |                 |                                    |                              |
   +----------------------------+-----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------+--------+-----------------+------------------------------------+------------------------------+
   | messages_remained          | Available Messages          | Number of messages that can be retrieved in the consumer group                                                                                                                 | >= 0                | Count  | N/A             | Consumer group of a Kafka instance | 1 minute                     |
   |                            |                             |                                                                                                                                                                                |                     |        |                 |                                    |                              |
   |                            |                             | This metric is available only when **Topic** is set to a specific topic name and **Monitoring Type** is set to **Partition monitoring** on the **By Consumer Group** tab page. |                     |        |                 |                                    |                              |
   +----------------------------+-----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------+--------+-----------------+------------------------------------+------------------------------+
   | topic_messages_remained    | Topic Available Messages    | Number of remaining messages that can be retrieved from the specified topic in the consumer group                                                                              | 0 to 2\ :sup:`63`-1 | Count  | N/A             | Consumer group of a Kafka instance | 1 minute                     |
   |                            |                             |                                                                                                                                                                                |                     |        |                 |                                    |                              |
   |                            |                             | This metric is available only when **Topic** is set to a specific topic name and **Monitoring Type** is set to **Basic monitoring** on the **By Consumer Group** tab page.     |                     |        |                 |                                    |                              |
   +----------------------------+-----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------+--------+-----------------+------------------------------------+------------------------------+
   | topic_messages_consumed    | Topic Retrieved Messages    | Number of messages that have been retrieved from the specified topic in the consumer group                                                                                     | 0 to 2\ :sup:`63`-1 | Count  | N/A             | Consumer group of a Kafka instance | 1 minute                     |
   |                            |                             |                                                                                                                                                                                |                     |        |                 |                                    |                              |
   |                            |                             | This metric is available only when **Topic** is set to a specific topic name and **Monitoring Type** is set to **Basic monitoring** on the **By Consumer Group** tab page.     |                     |        |                 |                                    |                              |
   +----------------------------+-----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------+--------+-----------------+------------------------------------+------------------------------+
   | consumer_messages_remained | Consumer Available Messages | Number of remaining messages that can be retrieved in the consumer group                                                                                                       | 0 to 2\ :sup:`63`-1 | Count  | N/A             | Consumer group of a Kafka instance | 1 minute                     |
   |                            |                             |                                                                                                                                                                                |                     |        |                 |                                    |                              |
   |                            |                             | This metric is available only when **Topic** is set to **All topics** on the **By Consumer Group** tab page.                                                                   |                     |        |                 |                                    |                              |
   +----------------------------+-----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------+--------+-----------------+------------------------------------+------------------------------+
   | consumer_messages_consumed | Consumer Retrieved Messages | Number of messages that have been retrieved in the consumer group                                                                                                              | 0 to 2\ :sup:`63`-1 | Count  | N/A             | Consumer group of a Kafka instance | 1 minute                     |
   |                            |                             |                                                                                                                                                                                |                     |        |                 |                                    |                              |
   |                            |                             | This metric is available only when **Topic** is set to **All topics** on the **By Consumer Group** tab page.                                                                   |                     |        |                 |                                    |                              |
   +----------------------------+-----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------+--------+-----------------+------------------------------------+------------------------------+

Smart Connect Metrics
---------------------

Smart Connect metrics are only available for cluster instances.

.. table:: **Table 5** Smart Connect metrics

   +-----------------------------+------------------------------+----------------------------------------------------------------------------------------+--------------------+--------+-----------------+----------------------------------------+------------------------------+
   | Metric ID                   | Metric Name                  | Description                                                                            | Value Range        | Unit   | Conversion Rule | Monitored Object (Dimension)           | Monitoring Period (Raw Data) |
   +=============================+==============================+========================================================================================+====================+========+=================+========================================+==============================+
   | kafka_wait_synchronize_data | Kafka Data to Sync           | Data to synchronize in the Kafka migration task                                        | >= 0               | Count  | N/A             | Smart Connect task of a Kafka instance | 1 minute                     |
   +-----------------------------+------------------------------+----------------------------------------------------------------------------------------+--------------------+--------+-----------------+----------------------------------------+------------------------------+
   | kafka_synchronize_rate      | Kafka Data Synced per Minute | Data synchronized per minute in the Kafka migration task                               | >= 0               | Count  | N/A             | Smart Connect task of a Kafka instance | 1 minute                     |
   +-----------------------------+------------------------------+----------------------------------------------------------------------------------------+--------------------+--------+-----------------+----------------------------------------+------------------------------+
   | task_status                 | Task Status                  | Status of the current task                                                             | -  **0**: abnormal | N/A    | N/A             | Smart Connect task of a Kafka instance | 1 minute                     |
   |                             |                              |                                                                                        | -  **1**: normal   |        |                 |                                        |                              |
   +-----------------------------+------------------------------+----------------------------------------------------------------------------------------+--------------------+--------+-----------------+----------------------------------------+------------------------------+
   | message_delay               | Message Delay                | Time elapsed between when a message is sent from the source and received by the target | >= 0               | ms     | N/A             | Smart Connect task of a Kafka instance | 1 minute                     |
   +-----------------------------+------------------------------+----------------------------------------------------------------------------------------+--------------------+--------+-----------------+----------------------------------------+------------------------------+

Precautions:

-  A Smart Connect task that bidirectionally copies Kafka data is split into two tasks for monitoring: *Smart Connect task name*\ **\_source_0** and *Smart Connect task name*\ **\_source_1**.
-  If all messages in a topic have aged before the next synchronization, there is no Kafka data to be synchronized. However, since the Kafka data synchronization metric uses the offset value that contains aged data, **Kafka Data Synced per Minute** will display the number of aged messages.

Dimension
---------

======================= ============================================
Key                     Value
======================= ============================================
kafka_instance_id       Kafka instance
kafka_broker            Kafka instance broker
kafka_topics            Kafka instance topic
kafka_partitions        Partition in a Kafka instance
kafka_groups-partitions Partition consumer group in a Kafka instance
kafka_groups_topics     Topic consumer group in a Kafka instance
kafka_groups            Consumer group of a Kafka instance
connector_task          Smart Connect task of a Kafka instance
======================= ============================================
