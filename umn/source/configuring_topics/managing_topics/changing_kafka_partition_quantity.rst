:original_name: kafka-ug-0006.html

.. _kafka-ug-0006:

Changing Kafka Partition Quantity
=================================

After creating a topic, you can change the number of partitions as required. Changing the number of partitions does **not** restart the instance or affect services.

Methods for changing the partition quantity:

-  :ref:`Repartitioning a Topic on the Console <kafka-ug-0006__section11349555102717>`
-  :ref:`Modifying Topic Partitions on the Client <kafka-ug-0006__section2227184716161>`

Notes and Constraints
---------------------

-  The number of partitions can only be increased.
-  The partition quantity of topics of a single-node or cluster Kafka instance is limited. **When the partition quantity limit is reached, you can no longer create topics.** The quantity varies with instance specifications. For details, see :ref:`Cluster Kafka Instances <kafka-specification>` and :ref:`Single-node Kafka Instances <kafka-pd-0056>`.
-  For an instance with ciphertext access enabled, if **allow.everyone.if.no.acl.found** is set to **false**, the topic partition quantity can be modified on the client only by the initial user (set in first ciphertext access enablement).

.. _kafka-ug-0006__section11349555102717:

Repartitioning a Topic on the Console
-------------------------------------

#. Log in to the console.

#. Click |image1| in the upper left corner to select the region where your instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click the desired instance to go to the instance details page.

#. In the navigation pane, choose **Topics**.

#. Modify the number of partitions using either of the following methods:

   -  Select one or more topics and click **Edit Topic** in the upper left corner.
   -  In the row containing the desired topic, click **Edit**.

#. In the **Edit Topic** dialog box, enter the number of partitions and click **OK**.

   To ensure performance, a maximum of 200 partitions is allowed for each topic on the Kafka console.

   View the partition quantity on the **Topics** page.

.. _kafka-ug-0006__section2227184716161:

Modifying Topic Partitions on the Client
----------------------------------------

If your Kafka client version is later than 2.2, you can use **kafka-topics.sh** to change the partition quantity.

-  For a Kafka instance with ciphertext access disabled, run the following command in the **/bin** directory of the Kafka client:

   .. code-block::

      ./kafka-topics.sh --bootstrap-server {connection-address} --topic {topic-name} --alter --partitions {number-of-partitions}

   .. table:: **Table 1** Topic partition quantity parameters

      +-----------------------------------+---------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                   |
      +===================================+===============================================================================================================+
      | connection-address                | Connection address of a Kafka instance. To obtain the address, choose **Basic Information** > **Connection**. |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------+
      | topic-name                        | Topic name.                                                                                                   |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------+
      | number-of-partitions              | Number of partitions in the topic.                                                                            |
      |                                   |                                                                                                               |
      |                                   | To ensure performance, **200 or less** partitions are recommended for each topic.                             |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------+

   Example:

   .. code-block:: console

      [root@ecs-kafka bin]# ./kafka-topics.sh --bootstrap-server 192.168.xx.xx:9092,192.168.xx.xx:9092,192.168.xx.xx:9092 --topic topic-01 --alter --partitions 6
      [root@ecs-kafka bin]#

-  For a Kafka instance with ciphertext access enabled, do as follows:

   #. (Optional) If the username and password, and the SSL certificate has been configured, skip this step and go to :ref:`2 <kafka-ug-0006__li529219395271>`. Otherwise, do as follows:

      Create the **ssl-user-config.properties** file in the **/config** directory of the Kafka client. Add the username and password, and the SSL certificate configuration by referring to :ref:`3 <kafka-ug-180801001__li5414277457>`.

   #. .. _kafka-ug-0006__li529219395271:

      Run the following command in the **/bin** directory of the Kafka client:

      .. code-block::

         ./kafka-topics.sh --bootstrap-server {connection-address} --topic {topic-name} --alter --partitions {number-of-partitions} --command-config ../config/{ssl-user-config.properties}

      .. table:: **Table 2** Topic partition quantity parameters

         +-----------------------------------+---------------------------------------------------------------------------------------------------------------+
         | Parameter                         | Description                                                                                                   |
         +===================================+===============================================================================================================+
         | connection-address                | Connection address of a Kafka instance. To obtain the address, choose **Basic Information** > **Connection**. |
         +-----------------------------------+---------------------------------------------------------------------------------------------------------------+
         | topic-name                        | Topic name.                                                                                                   |
         +-----------------------------------+---------------------------------------------------------------------------------------------------------------+
         | number-of-partitions              | Number of partitions in the topic.                                                                            |
         |                                   |                                                                                                               |
         |                                   | To ensure performance, **200 or less** partitions are recommended for each topic.                             |
         +-----------------------------------+---------------------------------------------------------------------------------------------------------------+
         | ssl-user-config.properties        | Configuration file name. This file contains username, password, and SSL certificate information.              |
         +-----------------------------------+---------------------------------------------------------------------------------------------------------------+

      Example:

      .. code-block:: console

         [root@ecs-kafka bin]# ./kafka-topics.sh --bootstrap-server 192.168.xx.xx:9093,192.168.xx.xx:9093,192.168.xx.xx:9093 --topic topic-01 --alter --partitions 6 --command-config ../config/ssl-user-config.properties
         [root@ecs-kafka bin]#

.. |image1| image:: /_static/images/en-us_image_0143929918.png
