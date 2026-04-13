:original_name: kafka-ug-0014.html

.. _kafka-ug-0014:

Viewing and Resetting Kafka Consumption Offsets
===============================================

A consumption offset indicates the consumption progress of a consumer. This section describes how to view and reset consumption offsets.

Notes and Constraints
---------------------

Messages may be consumed more than once after the offset is reset. Exercise caution when performing this operation.

Prerequisites
-------------

The consumer offset cannot be reset on the fly. You must first stop consumption of the desired consumer group. After a client is stopped, the server considers the client offline only after the time period specified in **ConsumerConfig.SESSION_TIMEOUT_MS_CONFIG** (1000 ms by default).

Viewing Consumer Offsets (Console)
----------------------------------

#. Log in to the console.
#. Click |image1| in the upper left corner to select the region where your instance is located.
#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.
#. Click the desired instance to go to the instance details page.
#. In the navigation pane, choose **Consumer Groups**.
#. Click the name of the desired consumer group.
#. On the **Consumer Offset** tab page, view the list of topics that the consumer group has subscribed to, topic quantity, total number of messages accumulated in the topic, and offset of each partition.

   .. table:: **Table 1** Consumer offset parameters

      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                                                                                                              |
      +===================================+==========================================================================================================================================================================================================================================================================================================+
      | Topic Name                        | Name of a topic that the consumer group has subscribed to                                                                                                                                                                                                                                                |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Partitions                        | Number of partitions in a topic                                                                                                                                                                                                                                                                          |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Cumulative Messages               | Number of messages that are not consumed by the consumer group in a topic                                                                                                                                                                                                                                |
      |                                   |                                                                                                                                                                                                                                                                                                          |
      |                                   | This parameter indicates the instantaneous value at the sampling. The value of its corresponding metric in monitoring is sampled every minute. These values may vary. For more information, see :ref:`Why Is the Number of Stacked Messages Monitored as 0 when Messages Are Stacked? <kafka-faq-0067>`. |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Partition                         | Partition number in a topic                                                                                                                                                                                                                                                                              |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Accumulated Messages              | Number of messages that are not consumed by the consumer group in a partition                                                                                                                                                                                                                            |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Offset                            | Offset of this partition                                                                                                                                                                                                                                                                                 |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Latest Offset                     | Maximum message position of a partition                                                                                                                                                                                                                                                                  |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | ID                                | ID of the consumer who consumes messages in this partition                                                                                                                                                                                                                                               |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Address                           | Address of the consumer who consumes messages in this partition                                                                                                                                                                                                                                          |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Client ID                         | Client identifier. This client is used to connect to a Kafka instance and consume messages in this partition.                                                                                                                                                                                            |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. (Optional) To query the consumer offsets of a specific topic, enter the topic name in the search box and press **Enter**.

Viewing Consumer Offsets (Kafka CLI)
------------------------------------

-  For a Kafka instance with ciphertext access disabled, run the following command in the **/bin** directory of the Kafka client:

   .. code-block::

      ./kafka-consumer-groups.sh --bootstrap-server ${connection-address} --offsets --describe --all-groups

   Parameter description: **connection-address** indicates the Kafka instance address, which can be obtained in the **Connection** area on the **Basic Information** page on the Kafka console.

   Example:

   .. code-block:: console

      [root@ecs-kafka bin]# ./kafka-consumer-groups.sh --bootstrap-server 192.168.xx.xx:9092,192.168.xx.xx:9092,192.168.xx.xx:9092 --offsets --describe --all-groups

      Consumer group '__consumer-group-dial-test' has no active members.

      GROUP                      TOPIC           PARTITION  CURRENT-OFFSET  LOG-END-OFFSET  LAG             CONSUMER-ID     HOST            CLIENT-ID
      __consumer-group-dial-test __dms_dial_test 0          350             350             0               -               -               -
      __consumer-group-dial-test __dms_dial_test 1          350             350             0               -               -               -
      __consumer-group-dial-test __dms_dial_test 2          350             350             0               -               -               -

      Consumer group 'test' has no active members.

      GROUP           TOPIC           PARTITION  CURRENT-OFFSET  LOG-END-OFFSET  LAG             CONSUMER-ID     HOST            CLIENT-ID
      test            topic-01        0          5               5               0               -               -               -
      test            topic-01        1          3               3               0               -               -               -
      test            topic-01        2          10              10              0               -               -               -
      [root@ecs-kafka bin]#

-  For a Kafka instance with ciphertext access enabled, do as follows:

   #. (Optional) If the username and password, and the SSL certificate has been configured, skip this step and go to :ref:`2 <kafka-ug-0014__li155191222323>`. Otherwise, do as follows:

      Create the **ssl-user-config.properties** file in the **/config** directory of the Kafka client. Add the username and password, and the SSL certificate configuration by referring to :ref:`3 <kafka-ug-180801001__li5414277457>`.

   #. .. _kafka-ug-0014__li155191222323:

      Run the following command in the **/bin** directory of the Kafka client:

      .. code-block::

         ./kafka-consumer-groups.sh --bootstrap-server {connection-address} --offsets --describe --all-groups --command-config ../config/{ssl-user-config.properties}

      .. table:: **Table 2** Consumer offset query parameters

         +----------------------------+---------------------------------------------------------------------------------------------------------------+
         | Parameter                  | Description                                                                                                   |
         +============================+===============================================================================================================+
         | connection-address         | Connection address of a Kafka instance. To obtain the address, choose **Basic Information** > **Connection**. |
         +----------------------------+---------------------------------------------------------------------------------------------------------------+
         | ssl-user-config.properties | Configuration file name. This file contains username, password, and SSL certificate information.              |
         +----------------------------+---------------------------------------------------------------------------------------------------------------+

      Example:

      .. code-block:: console

         [root@ecs-kafka bin]# ./kafka-consumer-groups.sh --bootstrap-server 192.168.xx.xx:9093,192.168.xx.xx:9093,192.168.xx.xx:9093 --offsets --describe --all-groups --command-config ../config/ssl-user-config.properties

         Consumer group '__consumer-group-dial-test' has no active members.

         GROUP                      TOPIC           PARTITION  CURRENT-OFFSET  LOG-END-OFFSET  LAG             CONSUMER-ID     HOST            CLIENT-ID
         __consumer-group-dial-test __dms_dial_test 0          347             347             0               -               -               -
         __consumer-group-dial-test __dms_dial_test 1          347             347             0               -               -               -
         __consumer-group-dial-test __dms_dial_test 2          347             347             0               -               -               -

         Consumer group 'test' has no active members.

         GROUP           TOPIC           PARTITION  CURRENT-OFFSET  LOG-END-OFFSET  LAG             CONSUMER-ID     HOST            CLIENT-ID
         test            topic-01        0          5               5               0               -               -               -
         test            topic-01        1          3               3               0               -               -               -
         test            topic-01        2          10              10              0               -               -               -
         [root@ecs-kafka bin]#

Resetting Consumer Offsets
--------------------------

#. Log in to the console.

#. Click |image2| in the upper left corner to select the region where your instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click the desired instance to go to the instance details page.

#. In the navigation pane, choose the **Consumer Groups** tab.

#. Click the name of the desired consumer group.

#. On the **Consumer Offset** tab page, you can perform the following operations:

   -  To reset the consumer offset of all partitions of a single topic, click **Reset Consumer Offset** in the row containing the desired topic.
   -  To reset the consumer offset of a single partition of a single topic, click **Reset Consumer Offset** in the row containing the desired partition.
   -  To reset the consumer offset of all partitions in all topics, click **One-touch Reset Consumer Offset**.

#. In the displayed **Reset Consumer Offset** dialog box, set the parameters by referring to :ref:`Table 3 <kafka-ug-0014__table13921162119239>`.

   .. _kafka-ug-0014__table13921162119239:

   .. table:: **Table 3** Parameters for resetting the consumer offset

      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                           |
      +===================================+=======================================================================================================================+
      | Reset By                          | You can reset an offset by:                                                                                           |
      |                                   |                                                                                                                       |
      |                                   | -  Time: Reset the offset to the specified time.                                                                      |
      |                                   | -  Offset: Reset the offset to the specified position.                                                                |
      |                                   |                                                                                                                       |
      |                                   | **Reset Consumer Offset** works with a specific time.                                                                 |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------+
      | Time                              | Set this parameter if **Reset By** is set to **Time**.                                                                |
      |                                   |                                                                                                                       |
      |                                   | Select a time point. After the reset is complete, retrieval starts from this time point.                              |
      |                                   |                                                                                                                       |
      |                                   | -  **Earliest**: earliest offset                                                                                      |
      |                                   | -  **Custom**: a custom time point                                                                                    |
      |                                   | -  **Latest**: latest offset                                                                                          |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------+
      | Offset                            | Set this parameter if **Reset By** is set to **Offset**.                                                              |
      |                                   |                                                                                                                       |
      |                                   | Enter an offset, which is greater than or equal to 0. After the reset is complete, retrieval starts from this offset. |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------+

#. Click **OK**.

#. Click **Yes** in the confirmation dialog box. The consumer offset is reset.

   On the **Consumer Offset** tab page, click |image3| before the topic whose consumer offset has been reset, and view the new value in the **Offset** column.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
.. |image2| image:: /_static/images/en-us_image_0143929918.png
.. |image3| image:: /_static/images/en-us_image_0000001160594580.png
