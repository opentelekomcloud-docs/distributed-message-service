:original_name: kafka-ug-0072.html

.. _kafka-ug-0072:

Modifying Kafka Topic Replicas
==============================

The replicas of a Kafka topic can be modified as required.

Reassigning partitions can modify replicas automatically or manually on the Kafka console. For more information, see :ref:`Modifying Replicas by Automatic Reassignment <kafka-ug-0072__section11229625184310>` and :ref:`Modifying Replicas by Manual Reassignment <kafka-ug-0072__section174151023194519>`.

Notes and Constraints
---------------------

-  Unavailable for single-node instances.
-  Reassignment tasks cannot be manually stopped. Please wait until they complete.
-  If partition reassignment has been scheduled, reassignment cannot be scheduled again for any topic in this instance until this reassignment is executed.

Operation Impact
----------------

-  Partition reassignment on topics with a large amount of data consumes a large amount of network and storage bandwidth. As a result, service requests may time out or the latency may increase. Therefore, you are advised to perform reassignment during off-peak hours. Compare the current instance load based on the instance specifications to decide whether the remaining instance capacity can support partition reassignment. Do not reassign partitions when there is insufficient bandwidth or when the CPU usage is greater than 90%. To view data volume and CPU usage of a topic, see **Message Size** and **CPU Usage** on the monitoring page. For details, see :ref:`Viewing Kafka Metrics <kafka-ug-190605001>`.
-  A throttle refers to the upper limit of the bandwidth for replication of a topic, to ensure that other topics on the instance are not affected. Note that throttles apply to replication triggered by both normal message production and partition reassignment. If the throttle is too small, normal message production may be affected, and partition reassignment may never complete. If partitions are continuously reassigned, contact customer service.
-  You cannot delete topics whose reassignment tasks have started. Otherwise, the tasks will never complete.
-  After partition reassignment, the metadata of the topic changes. If the producer does not support the retry mechanism, a few requests will fail, causing some messages to fail to be produced.
-  Reassignment takes longer for a topic with a large data volume. To check the volume, see the **Message Size** metric on the monitoring page by referring to :ref:`Viewing Kafka Metrics <kafka-ug-190605001>`. To reduce the amount of data to be migrated, :ref:`decrease the topic aging time <kafka-ug-200506001>` without affecting services and wait for messages to age. After the reassignment is complete, you can restore the aging time.

Prerequisite
------------

The target broker should have sufficient disk space. To check available disk space of each broker, see :ref:`Viewing Kafka Disk Usage <kafka-ug-0004>`. If the remaining disk capacity of the target broker is close to the amount of data to be migrated to the broker, :ref:`expand the disk capacity <kafka-ug-181221001>` before the reassignment.

.. _kafka-ug-0072__section11229625184310:

Modifying Replicas by Automatic Reassignment
--------------------------------------------

#. Log in to the console.

#. Click |image1| in the upper left corner to select the region where your instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click the desired instance to go to the instance details page.

#. In the navigation pane, choose **Topics**.

#. Go to the **Auto** page in either of the following ways:

   -  Select one or more topics and choose **Reassign** > **Auto** above the topic list.
   -  In the row containing the desired topic, choose **More** > **Reassign** > **Auto**.

#. Modify the replicas.

   .. table:: **Table 1** Parameters of automatic reassignment

      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                                                                                                                                                |
      +===================================+============================================================================================================================================================================================================================================================================================================================================+
      | Broker Name                       | Select the brokers to assign the topic's partition replicas to.                                                                                                                                                                                                                                                                            |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Replicas                          | Enter the number of replicas. This number must be less than or equal to the number of brokers.                                                                                                                                                                                                                                             |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Max. Bandwidth                    | Specify **throttle**. The default value is **-1**, indicating that there is no throttle.                                                                                                                                                                                                                                                   |
      |                                   |                                                                                                                                                                                                                                                                                                                                            |
      |                                   | If the instance has low workload (for example, only 30 of 300 MB/s is used), you are not advised to limit the bandwidth. Otherwise, you are advised to set it to a value greater than or equal to the total production bandwidth of the to-be-reassigned topic multiplied by the maximum number of replicas of the to-be-reassigned topic. |
      |                                   |                                                                                                                                                                                                                                                                                                                                            |
      |                                   | For details, see :ref:`Calculating a Throttle <kafka_ug_0023__section2847153373018>`.                                                                                                                                                                                                                                                      |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Execute                           | Specify when to execute the reassignment.                                                                                                                                                                                                                                                                                                  |
      |                                   |                                                                                                                                                                                                                                                                                                                                            |
      |                                   | -  **Now** means to execute it immediately.                                                                                                                                                                                                                                                                                                |
      |                                   | -  **As scheduled** means to execute it at the scheduled time.                                                                                                                                                                                                                                                                             |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. (Optional) Click **Calculate**. **Time Required** indicates how long automatic balancing will take.

   The one-click calculation function does not affect the performance of Kafka instances.

#. Click **OK**.

   The following table lists how to check whether reassignment is complete (scheduled and non-scheduled tasks):

   .. table:: **Table 2** Checking the reassignment result

      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Task Type                         | Reassignment Result                                                                                                                                                                                                                                             |
      +===================================+=================================================================================================================================================================================================================================================================+
      | Background tasks                  | In the upper left corner of the topic list, click **View details** and the **Background Tasks** > **Background tasks** page is displayed. The reassignment task is complete when it is in the **Successful** state, which means that the replicas are modified. |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Scheduled tasks                   | a. The **Background Tasks** > **Scheduled tasks** page is displayed. This page only shows whether scheduled tasks start to execute instead of whether they are successful.                                                                                      |
      |                                   |                                                                                                                                                                                                                                                                 |
      |                                   |    -  When the task status is **Pending**, reassignment has not been executed.                                                                                                                                                                                  |
      |                                   |    -  When the task status is **Successful**, reassignment has started.                                                                                                                                                                                         |
      |                                   |    -  When the task status is **Cancel**, reassignment has been canceled.                                                                                                                                                                                       |
      |                                   |                                                                                                                                                                                                                                                                 |
      |                                   | b. Click **Background tasks**. When the task status is **Successful**, reassignment has completed, which means that the replicas are modified.                                                                                                                  |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _kafka-ug-0072__section174151023194519:

Modifying Replicas by Manual Reassignment
-----------------------------------------

#. Log in to the console.

#. Click |image2| in the upper left corner to select the region where your instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click the desired instance to go to the instance details page.

#. In the navigation pane, choose **Topics**.

#. Go to the **Manual** page in either of the following ways:

   -  Select a topic and choose **Reassign** > **Manual** above the topic list. Manual reassignment does not support batch operations.
   -  In the row containing the desired topic, choose **More** > **Reassign** > **Manual**.

#. Modify the replicas.

   -  In the upper right corner of the **Manual** dialog box, click **Delete Replica** or **Add Replica** to reduce or increase the number of replicas for each partition of the topic.
   -  Under the name of the replica to be reassigned, click the broker name or |image3| and select the target broker to migrate the replica to. Assign replicas of the same partition to different brokers.
   -  Specify **throttle**. The default value is **-1**, indicating that there is no throttle. If the instance has low workload (for example, only 30 of 300 MB/s is used), you are not advised to limit the bandwidth. Otherwise, you are advised to set it to a value greater than or equal to the total production bandwidth of the to-be-reassigned topic multiplied by the maximum number of replicas of the to-be-reassigned topic. For details, see :ref:`Calculating a Throttle <kafka_ug_0023__section2847153373018>`.
   -  For **Execute**, specify when to execute the reassignment. **Now** means to execute it immediately. **As scheduled** means to execute it at the scheduled time.

#. (Optional) Click **Calculate**. **Time Required** indicates how long manual balancing will take.

   The one-click calculation function does not affect the performance of Kafka instances.

#. Click **OK**.

   The following table lists how to check whether reassignment is complete (scheduled and non-scheduled tasks):

   .. table:: **Table 3** Checking the reassignment result

      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Task Type                         | Reassignment Result                                                                                                                                                                                                                                             |
      +===================================+=================================================================================================================================================================================================================================================================+
      | Background tasks                  | In the upper left corner of the topic list, click **View details** and the **Background Tasks** > **Background tasks** page is displayed. The reassignment task is complete when it is in the **Successful** state, which means that the replicas are modified. |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Scheduled tasks                   | a. The **Background Tasks** > **Scheduled tasks** page is displayed. This page only shows whether scheduled tasks start to execute instead of whether they are successful.                                                                                      |
      |                                   |                                                                                                                                                                                                                                                                 |
      |                                   |    -  When the task status is **Pending**, reassignment has not been executed.                                                                                                                                                                                  |
      |                                   |    -  When the task status is **Successful**, reassignment has started.                                                                                                                                                                                         |
      |                                   |    -  When the task status is **Cancel**, reassignment has been canceled.                                                                                                                                                                                       |
      |                                   |                                                                                                                                                                                                                                                                 |
      |                                   | b. Click **Background tasks**. When the task status is **Successful**, reassignment has completed, which means that the replicas are modified.                                                                                                                  |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. |image1| image:: /_static/images/en-us_image_0143929918.png
.. |image2| image:: /_static/images/en-us_image_0143929918.png
.. |image3| image:: /_static/images/en-us_image_0000001453201733.png
