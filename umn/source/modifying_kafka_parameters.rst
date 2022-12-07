:original_name: kafka-ug-0007.html

.. _kafka-ug-0007:

Modifying Kafka Parameters
==========================

Scenario
--------

Your Kafka instances, topics, and consumers come with default configuration parameter settings. You can modify common parameters on the DMS console. For details about parameters that are not listed on the console, see the `Kafka official website <https://kafka.apache.org/documentation/#configuration>`__.

Parameters of v1.1.0 instances are all static parameters. v2.3.0/2.7 instances have both dynamic and static parameters.

-  Dynamic parameters: Modifying dynamic parameters will not restart the instance.
-  Static parameters: After static parameters are modified, you must manually restart the instance.

.. note::

   Configuration parameters of some old instances cannot be modified. Check whether your instance parameters can be modified on the console. If they cannot be modified, contact customer service.

Prerequisites
-------------

You can modify configuration parameters of a Kafka instance when the instance is in the **Running** state.

Procedure
---------

#. Log in to the management console.

#. Click |image1| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click the desired Kafka instance to view the instance details.

#. On the **Parameters** tab page, click **Edit** in the row containing the parameter to modify. :ref:`Table 1 <kafka-ug-0007__table131264453537>` describes the parameters of v1.1.0 instances. :ref:`Table 2 <kafka-ug-0007__table24142056192817>` and :ref:`Table 3 <kafka-ug-0007__table913673592919>` describe the parameters of v2.3.0/2.7 instances.

   .. _kafka-ug-0007__table131264453537:

   .. table:: **Table 1** Static parameters (v1.1.0 instances)

      +--------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+-----------------+
      | Parameter                      | Description                                                                                                                                                                                                                                                                             | Value Range           | Default Value   |
      +================================+=========================================================================================================================================================================================================================================================================================+=======================+=================+
      | min.insync.replicas            | If a producer sets the acks parameter to **all** (or **-1**), the **min.insync.replicas** parameter specifies the minimum number of replicas that must acknowledge a write for the write to be considered successful.                                                                   | 1-3                   | 1               |
      +--------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+-----------------+
      | message.max.bytes              | Maximum length of a single message, in bytes.                                                                                                                                                                                                                                           | 0-10,485,760          | 10,485,760      |
      +--------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+-----------------+
      | unclean.leader.election.enable | Indicates whether to allow replicas not in the ISR set to be elected as the leader as a last resort, even though doing so may result in data loss.                                                                                                                                      | **true** or **false** | true            |
      +--------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+-----------------+
      | connections.max.idle.ms        | Idle connection timeout (in ms). Connections that are idle for the duration specified by this parameter will be closed.                                                                                                                                                                 | 5000-600,000          | 600,000         |
      +--------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+-----------------+
      | log.retention.hours            | Duration (in hours) for retaining a log file.                                                                                                                                                                                                                                           | 1-168                 | 72              |
      |                                |                                                                                                                                                                                                                                                                                         |                       |                 |
      |                                | This parameter takes effect only for topics that have no aging time configured. If there is aging time configured for topics, it overrides this parameter.                                                                                                                              |                       |                 |
      +--------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+-----------------+
      | max.connections.per.ip         | The maximum number of connections allowed from each IP address. Request for new connections will be rejected once the limit is reached. The limit set using this parameter will be replaced if there are overrides configured using the **max.connections.per.ip.overrides** parameter. | 100-20,000            | 1000            |
      +--------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+-----------------+
      | group.max.session.timeout.ms   | The maximum session timeout (in ms) for consumers. A longer timeout gives consumers more time to process messages between heartbeats but results in a longer time to detect failures.                                                                                                   | 6000-1,800,000        | 1,800,000       |
      +--------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+-----------------+
      | default.replication.factor     | The default number of replicas configured for an automatically created topic.                                                                                                                                                                                                           | 1-3                   | 3               |
      +--------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+-----------------+
      | num.partitions                 | The default number of partitions configured for each automatically created topic.                                                                                                                                                                                                       | 1-100                 | 3               |
      +--------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+-----------------+
      | group.min.session.timeout.ms   | The minimum session timeout (in ms) for consumers. A shorter timeout enables quicker failure detection but results in more frequent consumer heartbeating, which can overwhelm broker resources.                                                                                        | 6000-300,000          | 6000            |
      +--------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+-----------------+

   .. _kafka-ug-0007__table24142056192817:

   .. table:: **Table 2** Dynamic parameters (v2.3.0/2.7 instances)

      +--------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+---------------+
      | Parameter                      | Description                                                                                                                                                                                                           | Value Range           | Default Value |
      +================================+=======================================================================================================================================================================================================================+=======================+===============+
      | min.insync.replicas            | If a producer sets the acks parameter to **all** (or **-1**), the **min.insync.replicas** parameter specifies the minimum number of replicas that must acknowledge a write for the write to be considered successful. | 1-3                   | 1             |
      +--------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+---------------+
      | message.max.bytes              | Maximum length of a single message, in bytes.                                                                                                                                                                         | 0-10,485,760          | 10,485,760    |
      +--------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+---------------+
      | unclean.leader.election.enable | Indicates whether to allow replicas not in the ISR set to be elected as the leader as a last resort, even though doing so may result in data loss.                                                                    | **true** or **false** | true          |
      +--------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+---------------+

   .. _kafka-ug-0007__table913673592919:

   .. table:: **Table 3** Static parameters (v2.3.0/2.7 instances)

      +------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------+-----------------+
      | Parameter                    | Description                                                                                                                                                                                                                                                                             | Value Range     | Default Value   |
      +==============================+=========================================================================================================================================================================================================================================================================================+=================+=================+
      | connections.max.idle.ms      | Idle connection timeout (in ms). Connections that are idle for the duration specified by this parameter will be closed.                                                                                                                                                                 | 5000-600,000    | 600,000         |
      +------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------+-----------------+
      | log.retention.hours          | Duration (in hours) for retaining a log file.                                                                                                                                                                                                                                           | 1-168           | 72              |
      |                              |                                                                                                                                                                                                                                                                                         |                 |                 |
      |                              | This parameter takes effect only for topics that have no aging time configured. If there is aging time configured for topics, it overrides this parameter.                                                                                                                              |                 |                 |
      +------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------+-----------------+
      | max.connections.per.ip       | The maximum number of connections allowed from each IP address. Request for new connections will be rejected once the limit is reached. The limit set using this parameter will be replaced if there are overrides configured using the **max.connections.per.ip.overrides** parameter. | 100-20,000      | 1000            |
      +------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------+-----------------+
      | group.max.session.timeout.ms | The maximum session timeout (in ms) for consumers. A longer timeout gives consumers more time to process messages between heartbeats but results in a longer time to detect failures.                                                                                                   | 6000-1,800,000  | 1,800,000       |
      +------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------+-----------------+
      | default.replication.factor   | The default number of replicas configured for an automatically created topic.                                                                                                                                                                                                           | 1-3             | 3               |
      +------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------+-----------------+
      | num.partitions               | The default number of partitions configured for each automatically created topic.                                                                                                                                                                                                       | 1-100           | 3               |
      +------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------+-----------------+
      | group.min.session.timeout.ms | The minimum session timeout (in ms) for consumers. A shorter timeout enables quicker failure detection but results in more frequent consumer heartbeating, which can overwhelm broker resources.                                                                                        | 6000-300,000    | 6000            |
      +------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------+-----------------+

   .. note::

      -  To modify multiple dynamic or static parameters at a time, click **Modify** above the parameter list.
      -  If you want to restore the default values, click **Restore Default** in the row containing the desired parameter.

#. Click **Save**.

   .. note::

      Modifying dynamic parameters will not restart the instance. **Static parameter modification requires manual restart of the instance.**

.. |image1| image:: /_static/images/en-us_image_0143929918.png
