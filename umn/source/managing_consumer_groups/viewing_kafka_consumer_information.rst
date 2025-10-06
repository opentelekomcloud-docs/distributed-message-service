:original_name: kafka-ug-0015.html

.. _kafka-ug-0015:

Viewing Kafka Consumer Information
==================================

If a consumer group has consumers who are accessing a Kafka instance, you can view their connection information.

Prerequisites
-------------

The consumer list and connection address can be viewed only when consumers in a consumer group are connected to the Kafka instance (that is, the consumer group is in the **STABLE** state).

Viewing the Consumer List (Console)
-----------------------------------

#. Log in to the console.

#. Click |image1| in the upper left corner to select the region where your instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click the desired instance to go to the instance details page.

#. In the navigation pane, choose **Consumer Groups**.

#. Click the name of the desired consumer group.

#. On the **Consumers** tab page, view the consumer list.

   In the consumer list, you can view the consumer ID, consumer address, and client ID.

#. (Optional) To query a specific consumer, enter the consumer ID in the search box and press **Enter**.

Viewing the Consumer List (Kafka CLI)
-------------------------------------

-  For a Kafka instance with ciphertext access disabled, run the following command in the **/bin** directory of the Kafka client:

   .. code-block::

      ./kafka-consumer-groups.sh --bootstrap-server {connection-address} --group {group-name} --members --describe

   .. table:: **Table 1** Consumer list query parameters

      +--------------------+---------------------------------------------------------------------------------------------------------------+
      | Parameter          | Description                                                                                                   |
      +====================+===============================================================================================================+
      | connection-address | Connection address of a Kafka instance. To obtain the address, choose **Basic Information** > **Connection**. |
      +--------------------+---------------------------------------------------------------------------------------------------------------+
      | group-name         | Consumer group name.                                                                                          |
      +--------------------+---------------------------------------------------------------------------------------------------------------+

   Example:

   .. code-block:: console

      [root@ecs-kafka bin]# ./kafka-consumer-groups.sh --bootstrap-server 192.168.xx.xx:9092,192.168.xx.xx:9092,192.168.xx.xx:9092 --group test --members --describe

      GROUP           CONSUMER-ID                                           HOST            CLIENT-ID        #PARTITIONS
      test            console-consumer-571a64fe-b0c4-47ce-833d-9e0da5a88d14 /192.168.0.215  console-consumer 3
      [root@ecs-kafka bin]#

-  For a Kafka instance with ciphertext access enabled, do as follows:

   #. (Optional) If the username and password, and the SSL certificate has been configured, skip this step and go to :ref:`2 <kafka-ug-0015__li85951698326>`. Otherwise, do as follows:

      Create the **ssl-user-config.properties** file in the **/config** directory of the Kafka client. Add the username and password, and the SSL certificate configuration by referring to :ref:`3 <kafka-ug-180801001__li5414277457>`.

   #. .. _kafka-ug-0015__li85951698326:

      Run the following command in the **/bin** directory of the Kafka client:

      .. code-block::

         ./kafka-consumer-groups.sh --bootstrap-server {connection-address} --group {group-name} --members --describe --command-config ../config/{ssl-user-config.properties}

      .. table:: **Table 2** Consumer list query parameters

         +----------------------------+---------------------------------------------------------------------------------------------------------------+
         | Parameter                  | Description                                                                                                   |
         +============================+===============================================================================================================+
         | connection-address         | Connection address of a Kafka instance. To obtain the address, choose **Basic Information** > **Connection**. |
         +----------------------------+---------------------------------------------------------------------------------------------------------------+
         | group-name                 | Consumer group name.                                                                                          |
         +----------------------------+---------------------------------------------------------------------------------------------------------------+
         | ssl-user-config.properties | Configuration file name. This file contains username, password, and SSL certificate information.              |
         +----------------------------+---------------------------------------------------------------------------------------------------------------+

      Example:

      .. code-block:: console

         [root@ecs-kafka bin]# ./kafka-consumer-groups.sh --bootstrap-server 192.168.xx.xx:9093,192.168.xx.xx:9093,192.168.xx.xx:9093 --group test --members --describe --command-config ../config/ssl-user-config.properties

         GROUP           CONSUMER-ID                                           HOST            CLIENT-ID        #PARTITIONS
         test            console-consumer-566d0c82-07d3-4d87-9a6e-f57a9bc9fc69 /192.168.0.215  console-consumer 3
         [root@ecs-kafka bin]#

Viewing Consumer Connection Addresses (Console)
-----------------------------------------------

#. Log in to the console.
#. Click |image2| in the upper left corner to select the region where your instance is located.
#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.
#. Click the desired instance to go to the instance details page.
#. In the navigation pane, choose **Consumer Groups**.
#. Click the desired consumer group.
#. On the **Consumers** tab page, view the consumer addresses.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
.. |image2| image:: /_static/images/en-us_image_0143929918.png
