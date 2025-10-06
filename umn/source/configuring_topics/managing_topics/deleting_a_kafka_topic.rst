:original_name: kafka-ug-180604019.html

.. _kafka-ug-180604019:

Deleting a Kafka Topic
======================

This document describes how to delete a topic.

-  :ref:`Deleting a Kafka Topic (Console) <kafka-ug-180604019__section0249155910409>`
-  :ref:`Deleting a Kafka Topic on the Client <kafka-ug-180604019__section98152410712>`

Notes and Constraints
---------------------

-  Deleting a topic clears the topic data permanently.
-  For an instance with ciphertext access enabled, if **allow.everyone.if.no.acl.found** is set to **false**, the topic can be deleted on the client only by the initial user (set in first ciphertext access enablement).

Prerequisite
------------

The instance is in the **Running** state.

.. _kafka-ug-180604019__section0249155910409:

Deleting a Kafka Topic (Console)
--------------------------------

#. Log in to the console.

#. Click |image1| in the upper left corner to select the region where your instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click the desired instance to go to the instance details page.

#. In the navigation pane, choose **Topics**.

#. Delete topics using either of the following methods:

   -  Select one or more topics and click **Delete Topic** in the upper left corner.
   -  In the row containing the topic you want to delete, choose **More** > **Delete**.

#. In the **Delete Topic** dialog box, click **OK**.

   The topic is deleted if it is not displayed in the topic list.

.. _kafka-ug-180604019__section98152410712:

Deleting a Kafka Topic on the Client
------------------------------------

If your Kafka client version is later than 2.2, you can use **kafka-topics.sh** to delete topics.

-  For a Kafka instance with ciphertext access disabled, run the following command in the **/bin** directory of the Kafka client:

   .. code-block::

      ./kafka-topics.sh --bootstrap-server {connection-address} --delete --topic {topic-name}

   .. table:: **Table 1** Topic deletion parameters

      +--------------------+---------------------------------------------------------------------------------------------------------------+
      | Parameter          | Description                                                                                                   |
      +====================+===============================================================================================================+
      | connection-address | Connection address of a Kafka instance. To obtain the address, choose **Basic Information** > **Connection**. |
      +--------------------+---------------------------------------------------------------------------------------------------------------+
      | topic-name         | Topic name.                                                                                                   |
      +--------------------+---------------------------------------------------------------------------------------------------------------+

   Example:

   .. code-block:: console

      [root@ecs-kafka bin]# ./kafka-topics.sh --bootstrap-server 192.168.xx.xx:9092,192.168.xx.xx:9092,192.168.xx.xx:9092 --delete --topic topic-01
      [root@ecs-kafka bin]#

-  For a Kafka instance with ciphertext access enabled, do as follows:

   #. (Optional) If the SSL certificate has been configured, skip this step and go to :ref:`2 <kafka-ug-180604019__li529219395271>`. Otherwise, do as follows:

      Create the **ssl-user-config.properties** file in the **/config** directory of the Kafka client and add the SSL certificate configurations by referring to :ref:`3 <kafka-ug-180801001__li5414277457>`.

   #. .. _kafka-ug-180604019__li529219395271:

      Run the following command in the **/bin** directory of the Kafka client:

      .. code-block::

         ./kafka-topics.sh --bootstrap-server {connection-address} --delete --topic {topic-name} --command-config ../config/{ssl-user-config.properties}

      .. table:: **Table 2** Topic deletion parameters

         +----------------------------+---------------------------------------------------------------------------------------------------------------+
         | Parameter                  | Description                                                                                                   |
         +============================+===============================================================================================================+
         | connection-address         | Connection address of a Kafka instance. To obtain the address, choose **Basic Information** > **Connection**. |
         +----------------------------+---------------------------------------------------------------------------------------------------------------+
         | topic-name                 | Topic name.                                                                                                   |
         +----------------------------+---------------------------------------------------------------------------------------------------------------+
         | ssl-user-config.properties | Configuration file name. This file contains username, password, and SSL certificate information.              |
         +----------------------------+---------------------------------------------------------------------------------------------------------------+

      Example:

      .. code-block:: console

         [root@ecs-kafka bin]# ./kafka-topics.sh --bootstrap-server 192.168.xx.xx:9093,192.168.xx.xx:9093,192.168.xx.xx:9093 --delete --topic topic-01 --command-config ../config/ssl-user-config.properties
         [root@ecs-kafka bin]#

.. |image1| image:: /_static/images/en-us_image_0143929918.png
