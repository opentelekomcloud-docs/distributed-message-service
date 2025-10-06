:original_name: kafka_ug_0021.html

.. _kafka_ug_0021:

Querying the Kafka Consumer Group List
======================================

After a consumer group is created, you can view its configuration and status.

Viewing the Consumer Group List (Console)
-----------------------------------------

#. Log in to the console.

#. Click |image1| in the upper left corner to select the region where your instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click the desired instance to go to the instance details page.

#. In the navigation pane, choose the **Consumer Groups** tab.

   The consumer group name, status, and Coordinator (ID) are displayed. Coordinator (ID) indicates the broker where the coordinator component is located. The consumer group status can be:

   -  **DEAD**: The consumer group has no member or metadata.
   -  **EMPTY**: The consumer group has metadata but has no member.
   -  **PREPARING_REBALANCE**: The consumer group is to be rebalanced.
   -  **COMPLETING_REBALANCE**: All members have joined the consumer group.
   -  **STABLE**: Members in the consumer group can consume messages normally.

#. (Optional) To query a consumer group, enter a consumer group name or status, Coordinator (ID), or keyword, then press **Enter**.

#. (Optional) To refresh the consumer group list, click |image2| in the upper right corner.

Viewing the Consumer Group List (Kafka CLI)
-------------------------------------------

-  For a Kafka instance with ciphertext access disabled, run the following command in the **/bin** directory of the Kafka client:

   .. code-block::

      ./kafka-consumer-groups.sh --bootstrap-server {connection-address} --list

   Parameter description: **connection-address** indicates the Kafka instance address, which can be obtained in the **Connection** area on the **Basic Information** page on the Kafka console.

   Example:

   .. code-block:: console

      [root@ecs-kafka bin]# ./kafka-consumer-groups.sh --bootstrap-server 192.168.xx.xx:9092,192.xx.xx.212:9092,192.xx.xx.147:9092 --list
      test
      __consumer-group-dial-test
      [root@ecs-kafka bin]#

-  For a Kafka instance with ciphertext access enabled, do as follows:

   #. (Optional) If the username and password, and the SSL certificate has been configured, skip this step and go to :ref:`2 <kafka_ug_0021__li529219395271>`. Otherwise, do as follows:

      Create the **ssl-user-config.properties** file in the **/config** directory of the Kafka client. Add the username and password, and the SSL certificate configuration by referring to :ref:`3 <kafka-ug-180801001__li5414277457>`.

   #. .. _kafka_ug_0021__li529219395271:

      Run the following command in the **/bin** directory of the Kafka client:

      .. code-block::

         ./kafka-consumer-groups.sh --bootstrap-server {connection-address} --list --command-config ../config/{ssl-user-config.properties}

      .. table:: **Table 1** Consumer group list query parameters

         +----------------------------+---------------------------------------------------------------------------------------------------------------+
         | Parameter                  | Description                                                                                                   |
         +============================+===============================================================================================================+
         | connection-address         | Connection address of a Kafka instance. To obtain the address, choose **Basic Information** > **Connection**. |
         +----------------------------+---------------------------------------------------------------------------------------------------------------+
         | ssl-user-config.properties | Configuration file name. This file contains username, password, and SSL certificate information.              |
         +----------------------------+---------------------------------------------------------------------------------------------------------------+

      Example:

      .. code-block:: console

         [root@ecs-kafka bin]# ./kafka-consumer-groups.sh --bootstrap-server 192.168.xx.xx:9093,192.168.xx.xx:9093,192.168.xx.xx:9093 --list --command-config ../config/ssl-user-config.properties
         test
         __consumer-group-dial-test
         [root@ecs-kafka bin]#

.. |image1| image:: /_static/images/en-us_image_0143929918.png
.. |image2| image:: /_static/images/en-us_image_0000001540501562.png
