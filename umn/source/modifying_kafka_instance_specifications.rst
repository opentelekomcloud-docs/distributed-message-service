:original_name: kafka-ug-181221001.html

.. _kafka-ug-181221001:

Modifying Kafka Instance Specifications
=======================================

Scenario
--------

After creating a Kafka instance, you can increase its specifications. :ref:`Table 1 <kafka-ug-181221001__table13500164702214>` lists available modification options. Only one object can be modified per operation: broker quantity, bandwidth, storage space, or broker flavor.

.. _kafka-ug-181221001__table13500164702214:

.. table:: **Table 1** Specification modification options

   ============== =============== ======== ========
   Old/New Flavor Modified Object Increase Decrease
   ============== =============== ======== ========
   New flavor     Broker quantity Y        x
   \              Storage space   Y        x
   \              Broker flavor   Y        x
   Old flavor     Bandwidth       Y        x
   \              Storage space   Y        x
   \              Broker flavor   x        x
   ============== =============== ======== ========

.. note::

   This function is unavailable for single-node instances.

**Distinguishing between old and new specifications:**

-  Old specifications: In the instance list, the instance specification is displayed as bandwidth (for example, **100 MB/s**).
-  New specifications: In the instance list, the instance specification is displayed as the ECS flavor multiplied by the number of brokers (for example, **kafka.2u4g.cluster*3 brokers**).


.. figure:: /_static/images/en-us_image_0000001803507917.png
   :alt: **Figure 1** Instance list

   **Figure 1** Instance list

Impact of Specification Modification
------------------------------------

It takes 5 to 10 minutes to modify specifications on one broker. The more brokers, the longer time the modification takes.

.. table:: **Table 2** Impact of specification modification

   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Modified Object                   | Impact                                                                                                                                                                                                                                                                                                                                                                                              |
   +===================================+=====================================================================================================================================================================================================================================================================================================================================================================================================+
   | Bandwidth or broker quantity      | -  Increasing the bandwidth or adding brokers does not affect the original brokers or services.                                                                                                                                                                                                                                                                                                     |
   |                                   | -  When you increase the bandwidth or change the broker quantity, the storage space is proportionally expanded based on the current disk space. For example, assume that the original number of brokers of an instance is 3 and the disk size of each broker is 200 GB. If the broker quantity changes to 10 and the disk size of each broker is still 200 GB, the total disk size becomes 2000 GB. |
   |                                   | -  New topics are created on new brokers, and the original topics are still on the original brokers, resulting in unbalanced partitions. You can :ref:`reassign partitions <kafka_ug_0023>` to migrate the replicas of the original topic partitions to the new brokers.                                                                                                                            |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Storage space                     | -  You can expand the storage space 20 times.                                                                                                                                                                                                                                                                                                                                                       |
   |                                   | -  Storage space expansion does not affect services.                                                                                                                                                                                                                                                                                                                                                |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Broker flavor                     | -  Single-replica topics do not support message production during this period. Services will be interrupted.                                                                                                                                                                                                                                                                                        |
   |                                   | -  If a topic has multiple replicas, modifying the broker flavor does not interrupt services, but may cause disorder of partition messages. Evaluate this impact and avoid peak hours.                                                                                                                                                                                                              |
   |                                   | -  Broker rolling restarts will cause partition leader changes, interrupting connections for less than a minute when the network is stable. For multi-replica topics, configure the retry mechanism on the producer client. To do so:                                                                                                                                                               |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                                     |
   |                                   |    -  If you use an open-source Kafka client, configure the **retries** parameter to a value in the range from 3 to 5.                                                                                                                                                                                                                                                                              |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                                     |
   |                                   |    -  If you use Flink, configure the retry policy by referring to the following code:                                                                                                                                                                                                                                                                                                              |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                                     |
   |                                   |       .. code-block::                                                                                                                                                                                                                                                                                                                                                                               |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                                     |
   |                                   |          StreamExecutionEnvironment env = StreamExecutionEnvironment.getExecutionEnvironment();                                                                                                                                                                                                                                                                                                     |
   |                                   |          env.setRestartStrategy(RestartStrategies.fixedDelayRestart(3, Time.seconds(20)));                                                                                                                                                                                                                                                                                                          |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Process of Increasing Broker Flavors
------------------------------------

When you scale up the broker flavor, a rolling restart is performed on brokers. The following process takes three brokers as an example:

#. .. _kafka-ug-181221001__li1034132713411:

   Stop the Kafka process on Broker 0.

#. Scale up the flavor of Broker 0.

#. .. _kafka-ug-181221001__li8548151418228:

   Restart the Kafka process on Broker 0.

#. Repeat :ref:`1 <kafka-ug-181221001__li1034132713411>` to :ref:`3 <kafka-ug-181221001__li8548151418228>` to scale up the flavor of Broker 1.

#. Repeat :ref:`1 <kafka-ug-181221001__li1034132713411>` to :ref:`3 <kafka-ug-181221001__li8548151418228>` to scale up the flavor of Broker 2.


.. figure:: /_static/images/en-us_image_0000001917432480.png
   :alt: **Figure 2** Process of increasing a broker flavor

   **Figure 2** Process of increasing a broker flavor


Modifying Kafka Instance Specifications
---------------------------------------

#. Log in to the console.

#. Click |image1| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. In the row containing the desired instance, choose **More** > **Modify Specifications** in the **Operation** column.

#. Specify the storage space, number of brokers, or broker flavor as required.

   **To modify old specifications, perform the following steps:**

   -  Increase the bandwidth.

      a. Specify a new bandwidth and click **Next**.
      b. Confirm the configurations and click **Submit**.
      c. Return to the instance list and check whether the change succeeded.

         -  If the instance status has changed from **Changing** to **Running**, the change succeeded. You can check the new bandwidth in the **Flavor** column.

         -  If the instance status has changed from **Changing** to **Change failed**, the change failed. Move the cursor over **Change failed** to check the failure cause.

            Instances in the **Change failed** state cannot be restarted, modified, or deleted. After the instance status automatically changes from **Change failed** to **Running**, you can continue to perform operations on the instance. If the status does not change to **Running**, contact customer service.

      .. note::

         After increasing the bandwidth, add the IP address of the new broker to the client connection configuration to improve reliability.

   -  Expand the storage space.

      a. Specify a new storage space and click **Next**.
      b. Confirm the configurations and click **Submit**.
      c. Return to the instance list and check whether the change succeeded.

         -  If the instance status has changed from **Changing** to **Running**, the change succeeded. View the new storage space (Storage space per broker x Number of brokers) in the **Used/Available Storage Space (GB)** column in the instance list.

         -  If the instance status has changed from **Changing** to **Change failed**, the change failed. Move the cursor over **Change failed** to check the failure cause.

            Instances in the **Change failed** state cannot be restarted, modified, or deleted. After the instance status automatically changes from **Change failed** to **Running**, you can continue to perform operations on the instance. If the status does not change to **Running**, contact customer service.

   **To modify new specifications, perform the following steps:**

   -  Expand the storage space.

      a. For **Change By**, select **Storage**. For **Storage Space per Broker**, specify a new storage space, and click **Next**. The storage space range varies by instance specifications. For details, see :ref:`Table 1 <kafka-specification__table152020206204>`.
      b. Confirm the configurations and click **Submit**.
      c. Return to the instance list and check whether the change succeeded.

         -  If the instance status has changed from **Changing** to **Running**, the change succeeded. View the new storage space (Storage space per broker x Number of brokers) in the **Used/Available Storage Space (GB)** column in the instance list.

         -  If the instance status has changed from **Changing** to **Change failed**, the change failed. Move the cursor over **Change failed** to check the failure cause.

            Instances in the **Change failed** state cannot be restarted, modified, or deleted. After the instance status automatically changes from **Change failed** to **Running**, you can continue to perform operations on the instance. If the status does not change to **Running**, contact customer service.

   -  Add brokers.

      a. For **Change By**, select **Brokers**. Then, enter the number of brokers and click **Next**. The broker quantity range varies by instance specifications. For details, see :ref:`Table 1 <kafka-specification__table152020206204>`. If public access has been enabled, configure EIPs for the new brokers. Then click **Next**.
      b. Confirm the configurations and click **Submit**.
      c. Return to the instance list and check whether the change succeeded.

         -  If the instance status has changed from **Changing** to **Running**, the change succeeded. You can check the new broker quantity in the **Flavor** column.

         -  If the instance status has changed from **Changing** to **Change failed**, the change failed. Move the cursor over **Change failed** to check the failure cause.

            Instances in the **Change failed** state cannot be restarted, modified, or deleted. After the instance status automatically changes from **Change failed** to **Running**, you can continue to perform operations on the instance. If the status does not change to **Running**, contact customer service.

      .. note::

         After adding brokers, add the IP addresses of the new brokers to the client connection configuration to improve reliability.

   -  Increase the broker flavor.

      a. For **Change By**, select **Broker Flavor**.

      b. Specify a new broker flavor.

      c. In the **Risk Check** area, check for risks.

         If any risk is found, handle it as prompted and click **Recheck**. If the risks do not need to be handled, select **I understand the risks.**

      d. Click **Next**, confirm the information, and click **Submit**.

      e. Return to the instance list and check whether the change succeeded.

         -  If the instance status has changed from **Changing** to **Running**, the change succeeded. You can check the new broker flavor in the **Flavor** column.

         -  If the instance status has changed from **Changing** to **Change failed**, the change failed. Move the cursor over **Change failed** to check the failure cause.

            Instances in the **Change failed** state cannot be restarted, modified, or deleted. After the instance status automatically changes from **Change failed** to **Running**, you can continue to perform operations on the instance. If the status does not change to **Running**, contact customer service.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
