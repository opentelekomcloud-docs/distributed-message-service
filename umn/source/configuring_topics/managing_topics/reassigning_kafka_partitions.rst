:original_name: kafka_ug_0023.html

.. _kafka_ug_0023:

Reassigning Kafka Partitions
============================

Scenario
--------

Partition reassignment is to reassign replicas of a partition to different brokers to solve the problem of unbalanced broker load.

Partition reassignment is required in the following scenarios:

-  After the broker quantity is increased for an instance, the replicas of the original topic partitions are migrated to the new brokers.
-  The leader partition is degraded to be a follower on a heavily loaded broker.
-  The number of replicas is increased or decreased.

The DMS for Kafka console provides automatic and manual reassignment. Automatic reassignment is recommended because it ensures that leaders are evenly distributed.

.. note::

   This function is unavailable for single-node instances.

Operation Impact
----------------

-  Partition reassignment on topics with a large amount of data consumes a large amount of network and storage bandwidth. As a result, service requests may time out or the latency may increase. Therefore, you are advised to perform reassignment during off-peak hours. Compare the current instance load based on the instance specifications to decide whether the remaining instance capacity can support partition reassignment. Do not reassign partitions when there is insufficient bandwidth or when the CPU usage is greater than 90%. To view data volume and CPU usage of a topic, see **Message Size** and **CPU Usage** on the monitoring page. For details, see :ref:`Viewing Kafka Monitoring Metrics <kafka-ug-190605001>`.
-  A throttle refers to the upper limit of the bandwidth for replication of a topic, to ensure that other topics on the instance are not affected. Note that throttles apply to replication triggered by both normal message production and partition reassignment. If the throttle is too small, normal message production may be affected, and partition reassignment may never complete. If partitions are continuously reassigned, contact customer service.
-  You cannot delete topics whose reassignment tasks have started. Otherwise, the tasks will never complete.
-  You cannot modify the partition quantity of topics whose reassignment tasks have started.
-  Reassignment tasks cannot be manually stopped. Please wait until they complete.
-  If partition reassignment has been scheduled, reassignment cannot be scheduled again for any topic in this instance until this reassignment is executed.
-  After partition reassignment, the metadata of the topic changes. If the producer does not support the retry mechanism, a few requests will fail, causing some messages to fail to be produced.
-  Reassignment takes a long time if the topic has a large amount of data. You are advised to :ref:`decrease the topic retention period <kafka-ug-200506001>` based on the topic consumption so that historical data of the topic can be deleted in a timely manner to accelerate the migration. To view data volume of a topic, see **Message Size** on the monitoring page. For details, see :ref:`Viewing Kafka Monitoring Metrics <kafka-ug-190605001>`.

Preparing for Partition Reassignment
------------------------------------

-  To reduce the amount of data to be migrated, :ref:`decrease the topic aging time <kafka-ug-200506001>` without affecting services and wait for messages to age. After the reassignment is complete, you can restore the aging time. To view data volume of a topic, see **Message Size** on the monitoring page. For details, see :ref:`Viewing Kafka Monitoring Metrics <kafka-ug-190605001>`.
-  The target broker should have sufficient disk space. To check available disk space of each broker, see :ref:`Viewing Kafka Disk Usage <kafka-ug-0004>`. If the remaining disk capacity of the target broker is close to the amount of data to be migrated to the broker, :ref:`expand the disk capacity <kafka-ug-181221001>` before the reassignment.

Auto Reassignment
-----------------

#. Log in to the console.

#. Click |image1| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click the desired Kafka instance to view the instance details.

#. In the navigation pane, choose the **Topics** tab.

#. Reassign partitions using either of the following methods:

   -  Select one or more topics and choose **Reassign** > **Auto** above the topic list.
   -  In the row that contains the desired topic, choose **More** > **Reassign** > **Auto**.

#. Set automatic reassignment parameters.

   -  In the **Brokers** area, select the brokers to assign the topic's partition replicas to.
   -  In the **Topics** area, enter the number of replicas to be automatically reassigned. The number of replicas must be less than or equal to the number of brokers.
   -  Specify **throttle**. The default value is **-1**, indicating that there is no throttle If the instance has low workload (for example, only 30/300 MB/s is used), you are not advised to limit the bandwidth. If a throttle is required, you are advised to set it to a value greater than or equal to the total production bandwidth of the to-be-reassigned topic multiplied by the maximum number of replicas of the to-be-reassigned topic. For details, see :ref:`Calculating a Throttle <kafka_ug_0023__section2847153373018>`.
   -  For **Execute**, specify when to execute the reassignment. **Now** means to execute it immediately. **As scheduled** means to execute it at the scheduled time.


   .. figure:: /_static/images/en-us_image_0000001940775828.png
      :alt: **Figure 1** Setting automatic reassignment parameters

      **Figure 1** Setting automatic reassignment parameters

#. (Optional) Click **Calculate**. **Time Required** indicates how long automatic balancing will take.

#. Click **OK**.

   The following table lists how to check whether reassignment is complete (scheduled and non-scheduled tasks):

   .. table:: **Table 1** Checking the reassignment result

      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Task Type                         | Reassignment Result                                                                                                                                                                                                 |
      +===================================+=====================================================================================================================================================================================================================+
      | Background tasks                  | In the upper left corner of the topic list, click **View details** and the **Background Tasks** > **Background tasks** page is displayed. The reassignment task is complete when it is in the **Successful** state. |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Scheduled tasks                   | a. The **Background Tasks** > **Scheduled tasks** page is displayed. This page only shows whether scheduled tasks start to execute instead of whether they are successful.                                          |
      |                                   |                                                                                                                                                                                                                     |
      |                                   |    -  When the task status is **Pending**, reassignment has not been executed.                                                                                                                                      |
      |                                   |    -  When the task status is **Successful**, reassignment has started.                                                                                                                                             |
      |                                   |    -  When the task status is **Cancel**, reassignment has been canceled.                                                                                                                                           |
      |                                   |                                                                                                                                                                                                                     |
      |                                   | b. Click **Background tasks** tab page. When the task status is **Successful**, reassignment has completed.                                                                                                         |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+


   .. figure:: /_static/images/en-us_image_0000001968058225.png
      :alt: **Figure 2** Background Tasks page

      **Figure 2** Background Tasks page

   .. note::

      -  You cannot delete topics whose reassignment tasks have started. Otherwise, the tasks will never complete.
      -  You cannot modify the partition quantity of topics whose reassignment tasks have started.
      -  Reassignment tasks cannot be manually stopped. Please wait until they complete.
      -  If partition reassignment has been scheduled, reassignment cannot be scheduled again for any topic in this instance until this reassignment is executed.

Manual Reassignment
-------------------

#. Log in to the console.

#. Click |image2| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click the desired Kafka instance to view the instance details.

#. In the navigation pane, choose the **Topics** tab.

#. Reassign partitions using either of the following methods:

   -  Select a topic and choose **Reassign** > **Manual** above the topic list. Manual reassignment does not support batch operations.
   -  In the row that contains the desired topic, choose **More** > **Reassign** > **Manual**.

#. Set manual reassignment parameters.

   -  In the upper right corner of the **Manual** dialog box, click **Delete Replica** or **Add Replica** to reduce or increase the number of replicas for each partition of the topic.
   -  Under the name of the replica to be reassigned, click the broker name or |image3| and select the target broker to migrate the replica to. Assign replicas of the same partition to different brokers.
   -  Specify **throttle**. The default value is **-1**, indicating that there is no throttle If the instance has low workload (for example, only 30/300 MB/s is used), you are not advised to limit the bandwidth. If a throttle is required, you are advised to set it to a value greater than or equal to the total production bandwidth of the to-be-reassigned topic multiplied by the maximum number of replicas of the to-be-reassigned topic. For details, see :ref:`Calculating a Throttle <kafka_ug_0023__section2847153373018>`.
   -  For **Execute**, specify when to execute the reassignment. **Now** means to execute it immediately. **As scheduled** means to execute it at the scheduled time.


   .. figure:: /_static/images/en-us_image_0000001940935336.png
      :alt: **Figure 3** Setting manual reassignment parameters

      **Figure 3** Setting manual reassignment parameters

#. (Optional) Click **Calculate**. **Time Required** indicates how long manual balancing will take.

#. Click **OK**.

   The following table lists how to check whether reassignment is complete (scheduled and non-scheduled tasks):

   .. table:: **Table 2** Checking the reassignment result

      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Task Type                         | Reassignment Result                                                                                                                                                                                                 |
      +===================================+=====================================================================================================================================================================================================================+
      | Background tasks                  | In the upper left corner of the topic list, click **View details** and the **Background Tasks** > **Background tasks** page is displayed. The reassignment task is complete when it is in the **Successful** state. |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Scheduled tasks                   | a. The **Background Tasks** > **Scheduled tasks** page is displayed. This page only shows whether scheduled tasks start to execute instead of whether they are successful.                                          |
      |                                   |                                                                                                                                                                                                                     |
      |                                   |    -  When the task status is **Pending**, reassignment has not been executed.                                                                                                                                      |
      |                                   |    -  When the task status is **Successful**, reassignment has started.                                                                                                                                             |
      |                                   |    -  When the task status is **Cancel**, reassignment has been canceled.                                                                                                                                           |
      |                                   |                                                                                                                                                                                                                     |
      |                                   | b. Click **Background tasks** tab page. When the task status is **Successful**, reassignment has completed.                                                                                                         |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+


   .. figure:: /_static/images/en-us_image_0000001968058225.png
      :alt: **Figure 4** Background Tasks page

      **Figure 4** Background Tasks page

   .. note::

      -  You cannot delete topics whose reassignment tasks have started. Otherwise, the tasks will never complete.
      -  You cannot modify the partition quantity of topics whose reassignment tasks have started.
      -  Reassignment tasks cannot be manually stopped. Please wait until they complete.
      -  If partition reassignment has been scheduled, reassignment cannot be scheduled again for any topic in this instance until this reassignment is executed.

Re-scheduling Partition Reassignment
------------------------------------

#. On the **Scheduled tasks** tab page on the **Background Tasks** page, click the drop-down box in the upper left corner, select a time period, enter the desired topic name in the search box, and press **Enter**.


   .. figure:: /_static/images/en-us_image_0000001968060361.png
      :alt: **Figure 5** Querying reassignment schedules

      **Figure 5** Querying reassignment schedules

#. In the row that contains the desired task, click **Modify**.

#. In the **Change Schedule** dialog box, change the schedule or cancel the scheduled task.

   -  To change the schedule, select a time and click **OK**.

   -  To cancel the task, select **Cancel** (as shown in :ref:`Figure 6 <kafka_ug_0023__fig1685184781212>`) and click **OK**.

      .. _kafka_ug_0023__fig1685184781212:

      .. figure:: /_static/images/en-us_image_0000001968997809.png
         :alt: **Figure 6** Canceling a scheduled reassignment task

         **Figure 6** Canceling a scheduled reassignment task

.. _kafka_ug_0023__section2847153373018:

Calculating a Throttle
----------------------

Throttles are affected by the execution duration of the reassignment, leader/follower distribution of partition replicas, and message production rate.

-  A throttle limits the replication traffic of all partitions in a broker.
-  Replicas added after the assignment are regarded as followers, and existing replicas are regarded as leaders. Throttles on leaders and followers are separated.
-  Throttles do not distinguish between replication caused by normal message production and that caused by partition reassignment. Therefore, the traffic generated in both cases is throttled.

Assume that the partition reassignment task needs to be completed within 200s and each replica has 100 MB data. Calculate the throttle in the following scenarios:

**Scenario 1: Topic 1 has two partitions and two replicas, and Topic 2 has one partition and one replica. All leader replicas are on the same broker. One replica needs to be added for Topic 1 and Topic 2 respectively.**

.. table:: **Table 3** Replica distribution before reassignment

   +------------+----------------+--------------------------+----------------------------+
   | Topic Name | Partition Name | Broker of Leader Replica | Broker of Follower Replica |
   +============+================+==========================+============================+
   | Topic 1    | 0              | 0                        | 0, 1                       |
   +------------+----------------+--------------------------+----------------------------+
   | Topic 1    | 1              | 0                        | 0, 2                       |
   +------------+----------------+--------------------------+----------------------------+
   | Topic 2    | 0              | 0                        | 0                          |
   +------------+----------------+--------------------------+----------------------------+

.. table:: **Table 4** Replica distribution after reassignment

   +------------+----------------+--------------------------+----------------------------+
   | Topic Name | Partition Name | Broker of Leader Replica | Broker of Follower Replica |
   +============+================+==========================+============================+
   | Topic 1    | 0              | 0                        | 0, 1, 2                    |
   +------------+----------------+--------------------------+----------------------------+
   | Topic 1    | 1              | 0                        | 0, 1, 2                    |
   +------------+----------------+--------------------------+----------------------------+
   | Topic 2    | 0              | 0                        | 0, 2                       |
   +------------+----------------+--------------------------+----------------------------+

.. _kafka_ug_0023__fig11847155234519:

.. figure:: /_static/images/en-us_image_0000001403219302.png
   :alt: **Figure 7** Reassignment scenario 1

   **Figure 7** Reassignment scenario 1

As shown in :ref:`Figure 7 <kafka_ug_0023__fig11847155234519>`, three replicas fetch data from Broker 0. Each replica on Broker 0 has 100 MB data. Broker 0 has only leader replicas, and Broker 1 and Broker 2 have only follower replicas.

-  Bandwidth required by Broker 0 to complete partition reassignment within 200s = (100 MB + 100 MB + 100 MB)/200s = 1.5 MB/s
-  Bandwidth required by Broker 1 to complete partition reassignment within 200s = 100 MB/200s = 0.5 MB/s
-  Bandwidth required by Broker 2 to complete partition reassignment within 200s = (100 MB + 100 MB)/200s = 1 MB/s

In conclusion, to complete the partition reassignment task within 200s, set the throttle to a value greater than or equal to 1.5 MB/s. The bandwidth should be set to be greater than or equal to 2 MB/s because the limit on it on the console must be an integer.

**Scenario 2: Topic 1 has two partitions and one replica, and Topic 2 has two partitions and one replica. Leader replicas are on different brokers. One replica needs to be added for Topic 1 and Topic 2 respectively.**

.. table:: **Table 5** Replica distribution before reassignment

   +------------+----------------+--------------------------+----------------------------+
   | Topic Name | Partition Name | Broker of Leader Replica | Broker of Follower Replica |
   +============+================+==========================+============================+
   | Topic 1    | 0              | 0                        | 0                          |
   +------------+----------------+--------------------------+----------------------------+
   | Topic 1    | 1              | 1                        | 1                          |
   +------------+----------------+--------------------------+----------------------------+
   | Topic 2    | 0              | 1                        | 1                          |
   +------------+----------------+--------------------------+----------------------------+
   | Topic 2    | 1              | 2                        | 2                          |
   +------------+----------------+--------------------------+----------------------------+

.. table:: **Table 6** Replica distribution after reassignment

   +------------+----------------+--------------------------+----------------------------+
   | Topic Name | Partition Name | Broker of Leader Replica | Broker of Follower Replica |
   +============+================+==========================+============================+
   | Topic 1    | 0              | 0                        | 0, 2                       |
   +------------+----------------+--------------------------+----------------------------+
   | Topic 1    | 1              | 1                        | 1, 2                       |
   +------------+----------------+--------------------------+----------------------------+
   | Topic 2    | 0              | 1                        | 1, 2                       |
   +------------+----------------+--------------------------+----------------------------+
   | Topic 2    | 1              | 2                        | 2, 0                       |
   +------------+----------------+--------------------------+----------------------------+

.. _kafka_ug_0023__fig03691046202512:

.. figure:: /_static/images/en-us_image_0000001404290946.png
   :alt: **Figure 8** Reassignment scenario 2

   **Figure 8** Reassignment scenario 2

As shown in :ref:`Figure 8 <kafka_ug_0023__fig03691046202512>`, Broker 1 has only leader replicas, and Broker 0 and Broker 2 have both leader and follower replicas. Leader and follower replicas on Broker 0 and Broker 2 are throttled separately.

-  Bandwidth required by Broker 0 (leader) to complete partition reassignment within 200s = 100 MB/200s = 0.5 MB/s
-  Bandwidth required by Broker 0 (follower) to complete partition reassignment within 200s = 100 MB/200s = 0.5 MB/s
-  Bandwidth required by Broker 1 to complete partition reassignment within 200s = (100 MB + 100 MB)/200s = 1 MB/s
-  Bandwidth required by Broker 2 (leader) to complete partition reassignment within 200s = 100 MB/200s = 0.5 MB/s
-  Bandwidth required by Broker 2 (follower) to complete partition reassignment within 200s = (100 MB + 100 MB + 100 MB)/200s = 1.5 MB/s

In conclusion, to complete the partition reassignment task within 200s, set the throttle to a value greater than or equal to 1.5 MB/s. The bandwidth should be set to be greater than or equal to 2 MB/s because the limit on it on the console must be an integer.

**Scenario 3: Both Topic 1 and Topic 2 have one partition and two replicas. All leader replicas are on the same broker. One replica needs to be added to Topic 1. Messages are produced on Topic 1, causing replication.**

.. table:: **Table 7** Replica distribution before reassignment

   +------------+----------------+--------------------------+----------------------------+
   | Topic Name | Partition Name | Broker of Leader Replica | Broker of Follower Replica |
   +============+================+==========================+============================+
   | Topic 1    | 0              | 0                        | 0, 1                       |
   +------------+----------------+--------------------------+----------------------------+
   | Topic 2    | 0              | 0                        | 0, 1                       |
   +------------+----------------+--------------------------+----------------------------+

.. table:: **Table 8** Replica distribution after reassignment

   +------------+----------------+--------------------------+----------------------------+
   | Topic Name | Partition Name | Broker of Leader Replica | Broker of Follower Replica |
   +============+================+==========================+============================+
   | Topic 1    | 0              | 0                        | 0, 1, 2                    |
   +------------+----------------+--------------------------+----------------------------+
   | Topic 2    | 0              | 0                        | 0, 1                       |
   +------------+----------------+--------------------------+----------------------------+

.. _kafka_ug_0023__fig1059214198291:

.. figure:: /_static/images/en-us_image_0000001454518289.png
   :alt: **Figure 9** Reassignment scenario 3

   **Figure 9** Reassignment scenario 3

As shown in :ref:`Figure 9 <kafka_ug_0023__fig1059214198291>`, one replica needs to fetch data from Broker 0 for partition reassignment, and the other replica needs to fetch data from Broker 0 for message production. Since the throttle does not distinguish between message production and partition reassignment, the traffic caused by both is limited and counted.

-  Bandwidth required by Broker 0 to complete partition reassignment within 200s = (100 MB + 700 KB/s x 200s)/200s + 700 KB/s= 1.9 MB/s
-  Bandwidth required by Broker 2 to complete partition reassignment within 200s = 100 MB/200s = 0.5 MB/s

In conclusion, to complete the partition reassignment task within 200s, set the throttle to a value greater than or equal to 1.9 MB/s. The bandwidth should be set to be greater than or equal to 2 MB/s because the limit on it on the console must be an integer.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
.. |image2| image:: /_static/images/en-us_image_0143929918.png
.. |image3| image:: /_static/images/en-us_image_0000001453201733.png
