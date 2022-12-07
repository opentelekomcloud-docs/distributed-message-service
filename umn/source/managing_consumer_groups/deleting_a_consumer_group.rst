:original_name: kafka-ug-0012.html

.. _kafka-ug-0012:

Deleting a Consumer Group
=========================

You can delete a consumer group using either of the following methods:

-  Method 1: Delete a consumer group on the console.
-  Method 2: Use `Kafka CLI <https://cwiki.apache.org/confluence/display/KAFKA/Clients>`__ to delete a consumer group. (Ensure that the Kafka instance version is the same as the CLI version.)

Prerequisites
-------------

The status of the consumer group to be deleted is **EMPTY**.

Method 1: Deleting a Consumer Group on the Console
--------------------------------------------------

#. Log in to the management console.

#. Click |image1| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click the desired Kafka instance to view the instance details.

#. In the navigation pane, choose the **Consumer Groups** tab.

#. Delete consumer groups using either of the following methods:

   -  Select one or more consumer groups and click **Delete Consumer Group** above the consumer group list.
   -  In the row containing the consumer group you want to delete, click **Delete**.

   .. important::

      A consumer group can be deleted only when its status is **EMPTY**.

   Consumer group statuses include:

   -  **DEAD**: The consumer group has no member or metadata.
   -  **EMPTY**: The consumer group has metadata but has no member.
   -  **PREPARING_REBALANCE**: The consumer group is to be rebalanced.
   -  **COMPLETING_REBALANCE**: All members have joined the consumer group.
   -  **STABLE**: Members in the consumer group can consume messages normally.

#. In the displayed **Delete Consumer Group** dialog box, click **Yes**.

Method 2: Using the CLI to Delete a Consumer Group
--------------------------------------------------

The following uses Linux as an example.

#. Download Kafka CLI `v1.1.0 <https://archive.apache.org/dist/kafka/1.1.0/kafka_2.11-1.1.0.tgz>`__, `v2.7.2 <https://archive.apache.org/dist/kafka/2.7.2/kafka_2.12-2.7.2.tgz>`__, or `v2.3.0 <https://archive.apache.org/dist/kafka/2.3.0/kafka_2.11-2.3.0.tgz>`__. Ensure that the Kafka instance and the CLI are of the same version.

#. Use the CLI to connect to the Kafka instance. For details, see :ref:`Accessing a Kafka Instance Without SASL <kafka-ug-180604020>` or :ref:`Accessing a Kafka Instance with SASL <kafka-ug-180801001>`.

#. In the **/**\ *{directory where the CLI is located}*\ **/kafka\_**\ *{version}*\ **/bin/** directory, run the following command to delete a consumer group:

   **kafka-consumer-groups.sh --bootstrap-server** *{Kafka instance connection address}* **--delete --group** *{consumer group name}*

   .. code-block:: console

      [root@zk-server-1 bin]# ./kafka-consumer-groups.sh --bootstrap-server 192.168.1.245:9091,192.168.1.86:9091,192.168.1.128:9091 --delete --group bbbb
      Note: This will not show information about old Zookeeper-based consumers.
      Deletion of requested consumer groups ('bbbb') was successful.

   .. note::

      If SASL authentication is enabled for the Kafka instance, the **--command-config {consumer.properties file with SASL authentication}** parameter must be added to the preceding commands. For details about the **consumer.properties** file, see :ref:`Accessing a Kafka Instance with SASL <kafka-ug-180801001>`.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
