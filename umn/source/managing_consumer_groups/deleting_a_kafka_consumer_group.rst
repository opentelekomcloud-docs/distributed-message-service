:original_name: kafka-ug-0012.html

.. _kafka-ug-0012:

Deleting a Kafka Consumer Group
===============================

You can delete a consumer group in either of the following ways:

-  On the console.
-  Use `Kafka CLI <https://cwiki.apache.org/confluence/display/KAFKA/Clients>`__. (Ensure that the Kafka instance version is the same as the CLI version.)

Notes and Constraints
---------------------

-  If **auto.create.groups.enable** is set to **true**, the consumer group status is **EMPTY**, and no offset has been submitted, the system automatically deletes the consumer group 10 minutes later.
-  If **auto.create.groups.enable** is set to **false**, the system does not automatically delete consumer groups. You can manually delete them.
-  If a consumer group has never committed an offset, the group will be deleted after the Kafka instance restarts.
-  Deleting a consumer group loses the consumption offset. Re-consumption or repeated consumption may occur.

Prerequisite
------------

The status of the consumer group to be deleted is **EMPTY**.

Deleting a Consumer Group (Console)
-----------------------------------

#. Log in to the console.

#. Click |image1| in the upper left corner to select the region where your instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click the desired instance to go to the instance details page.

#. In the navigation pane, choose **Consumer Groups**.

#. Delete consumer groups using either of the following methods:

   -  Select one or more consumer groups and click **Delete Consumer Group** above the consumer group list.
   -  In the row containing the consumer group to be deleted, click **Delete**.
   -  Click the consumer group to be deleted. The consumer group details page is displayed. Click **Delete** in the upper right corner.

#. In the displayed **Delete Consumer Group** dialog box, click **OK**.

   The consumer groups are deleted when they are no longer displayed in the consumer group list.

Deleting a Consumer Group (Kafka Client)
----------------------------------------

The following uses Linux as an example.

-  For a Kafka instance with ciphertext access disabled, run the following command in the **/bin** directory of the Kafka client:

   .. code-block::

      ./kafka-consumer-groups.sh --bootstrap-server {connection-address} --delete --group {group-name}

   .. table:: **Table 1** Consumer group deletion parameters

      +--------------------+---------------------------------------------------------------------------------------------------------------+
      | Parameter          | Description                                                                                                   |
      +====================+===============================================================================================================+
      | connection-address | Connection address of a Kafka instance. To obtain the address, choose **Basic Information** > **Connection**. |
      +--------------------+---------------------------------------------------------------------------------------------------------------+
      | group-name         | Consumer group name.                                                                                          |
      +--------------------+---------------------------------------------------------------------------------------------------------------+

   Example:

   .. code-block:: console

      [root@ecs-kafka bin]# ./kafka-consumer-groups.sh --bootstrap-server 192.168.xx.xx:9092,192.168.xx.xx:9092,192.168.xx.xx:9092 --delete --group group-01
      Deletion of requested consumer groups ('group-01') was successful.
      [root@ecs-kafka bin]#

-  For a Kafka instance with ciphertext access enabled, do as follows:

   #. (Optional) If the SSL certificate has been configured, skip this step and go to :ref:`2 <kafka-ug-0012__li529219395271>`. Otherwise, do as follows:

      Create the **ssl-user-config.properties** file in the **/config** directory of the Kafka client and add the SSL certificate configurations by referring to :ref:`3 <kafka-ug-180801001__li5414277457>`.

   #. .. _kafka-ug-0012__li529219395271:

      In the **/bin** directory of the Kafka client, run the following command:

      .. code-block::

         ./kafka-consumer-groups.sh --bootstrap-server {connection-address} --delete --group {group-name} --command-config ../config/{ssl-user-config.properties}

      .. table:: **Table 2** Consumer group deletion parameters

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

         [root@ecs-kafka bin]# ./kafka-consumer-groups.sh --bootstrap-server 192.168.xx.xx:9093,192.168.xx.xx:9093,192.168.xx.xx:9093 --delete --group group-02 --command-config ../config/ssl-user-config.properties
         Deletion of requested consumer groups ('group-02') was successful.
         [root@ecs-kafka bin]#

.. |image1| image:: /_static/images/en-us_image_0143929918.png
