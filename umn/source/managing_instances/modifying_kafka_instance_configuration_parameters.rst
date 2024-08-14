:original_name: kafka-ug-0007.html

.. _kafka-ug-0007:

Modifying Kafka Instance Configuration Parameters
=================================================

Your Kafka instances, topics, and consumers come with default configuration parameter settings. You can modify common parameters on the DMS console. For details about parameters that are not listed on the console, see the `Kafka official website <https://kafka.apache.org/documentation/#configuration>`__.

Kafka instances have dynamic and static parameters:

-  Dynamic parameters: Modifying dynamic parameters will not restart the instance.
-  Static parameters: After static parameters are modified, you must manually restart the instance.

.. note::

   -  Configuration parameters of some old instances cannot be modified. Check whether your instance parameters can be modified on the console. If they cannot be modified, contact customer service.
   -  This function is not available for single-node instances.

Prerequisites
-------------

You can modify configuration parameters of a Kafka instance when the instance is in the **Running** state.

Procedure
---------

#. Log in to the console.

#. Click |image1| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click the desired Kafka instance to view the instance details.

#. On the **Parameters** page, click **Edit** in the row containing the parameter to modify.

   Parameters of v1.1.0 instances are described in :ref:`Table 1 <kafka-ug-0007__table1037720402179>` and :ref:`Table 2 <kafka-ug-0007__table131264453537>`. Parameters of v2.3.0/v2.7/3.x instances are described in :ref:`Table 3 <kafka-ug-0007__table24142056192817>` and :ref:`Table 4 <kafka-ug-0007__table913673592919>`.

   .. _kafka-ug-0007__table1037720402179:

   .. table:: **Table 1** Dynamic parameters (v1.1.0 instances)

      +---------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------+-----------------+
      | Parameter                 | Description                                                                                                                                                                                                                                                  | Value Range     | Default Value   |
      +===========================+==============================================================================================================================================================================================================================================================+=================+=================+
      | auto.create.groups.enable | Whether to automatically create consumer groups.                                                                                                                                                                                                             | true/false      | true            |
      |                           |                                                                                                                                                                                                                                                              |                 |                 |
      |                           | This parameter is not displayed on the console for some earlier instances. The function of automatically creating consumer groups is enabled by default and cannot be disabled on the console.                                                               |                 |                 |
      +---------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------+-----------------+
      | offsets.retention.minutes | The longest period a consumption position can be retained starts from the time of submission. Positions retained beyond this duration will be deleted. Each time a consumption position is submitted to a topic partition, its retention period resets to 0. | 1440-30240      | 20160           |
      |                           |                                                                                                                                                                                                                                                              |                 |                 |
      |                           | This parameter is displayed as a static one for certain earlier instances.                                                                                                                                                                                   | Unit: minute    |                 |
      +---------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------+-----------------+

   .. _kafka-ug-0007__table131264453537:

   .. table:: **Table 2** Static parameters (v1.1.0 instances)

      +--------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+-----------------+
      | Parameter                      | Description                                                                                                                                                                                                           | Value Range           | Default Value   |
      +================================+=======================================================================================================================================================================================================================+=======================+=================+
      | min.insync.replicas            | If a producer sets the acks parameter to **all** (or **-1**), the **min.insync.replicas** parameter specifies the minimum number of replicas that must acknowledge a write for the write to be considered successful. | 1-3                   | 1               |
      +--------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+-----------------+
      | message.max.bytes              | Maximum length of a single message.                                                                                                                                                                                   | 0-10,485,760          | 10,485,760      |
      |                                |                                                                                                                                                                                                                       |                       |                 |
      |                                |                                                                                                                                                                                                                       | Unit: byte            |                 |
      +--------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+-----------------+
      | unclean.leader.election.enable | Indicates whether to allow replicas not in the ISR set to be elected as the leader as a last resort, even though doing so may result in data loss.                                                                    | **true** or **false** | false           |
      +--------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+-----------------+
      | connections.max.idle.ms        | Idle connection timeout (in ms). Connections that are idle for the duration specified by this parameter will be closed.                                                                                               | 5000-600,000          | 600,000         |
      |                                |                                                                                                                                                                                                                       |                       |                 |
      |                                |                                                                                                                                                                                                                       | Unit: millisecond     |                 |
      +--------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+-----------------+
      | log.retention.hours            | Maximum duration for storing log files.                                                                                                                                                                               | 1-168                 | 72              |
      |                                |                                                                                                                                                                                                                       |                       |                 |
      |                                | This parameter takes effect only for topics that have no aging time configured. If there is aging time configured for topics, it overrides this parameter.                                                            | Unit: hour            |                 |
      +--------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+-----------------+
      | max.connections.per.ip         | The maximum number of connections allowed from each IP address. Request for new connections will be rejected once the limit is reached.                                                                               | 100-20,000            | 1000            |
      +--------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+-----------------+
      | group.max.session.timeout.ms   | Maximum session timeout for consumers. A longer timeout gives consumers more time to process messages between heartbeats but results in a longer time to detect failures.                                             | 6000-1,800,000        | 1,800,000       |
      |                                |                                                                                                                                                                                                                       |                       |                 |
      |                                |                                                                                                                                                                                                                       | Unit: millisecond     |                 |
      +--------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+-----------------+
      | default.replication.factor     | The default number of replicas configured for an automatically created topic.                                                                                                                                         | 1-3                   | 3               |
      +--------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+-----------------+
      | allow.everyone.if.no.acl.found | When this parameter is set to **true**, all users can access resources without ACL rules.                                                                                                                             | true/false            | true            |
      |                                |                                                                                                                                                                                                                       |                       |                 |
      |                                | This parameter is displayed only when is enabled for the instance or ciphertext access is used.                                                                                                                       |                       |                 |
      |                                |                                                                                                                                                                                                                       |                       |                 |
      |                                | This parameter cannot be modified for certain earlier instances.                                                                                                                                                      |                       |                 |
      +--------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+-----------------+
      | num.partitions                 | The default number of partitions configured for each automatically created topic.                                                                                                                                     | 1-200                 | 3               |
      +--------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+-----------------+
      | group.min.session.timeout.ms   | Minimum session timeout for consumers. A shorter timeout enables quicker failure detection but results in more frequent consumer heartbeating, which can overwhelm broker resources.                                  | 6000-300,000          | 6000            |
      |                                |                                                                                                                                                                                                                       |                       |                 |
      |                                |                                                                                                                                                                                                                       | Unit: millisecond     |                 |
      +--------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+-----------------+

   .. _kafka-ug-0007__table24142056192817:

   .. table:: **Table 3** Dynamic parameters (2.3.0/2.7/3.x instances)

      +--------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+-----------------+
      | Parameter                      | Description                                                                                                                                                                                                                                                  | Value Range           | Default Value   |
      +================================+==============================================================================================================================================================================================================================================================+=======================+=================+
      | min.insync.replicas            | If a producer sets the acks parameter to **all** (or **-1**), the **min.insync.replicas** parameter specifies the minimum number of replicas that must acknowledge a write for the write to be considered successful.                                        | 1-3                   | 1               |
      +--------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+-----------------+
      | message.max.bytes              | Maximum length of a single message.                                                                                                                                                                                                                          | 0-10,485,760          | 10,485,760      |
      |                                |                                                                                                                                                                                                                                                              |                       |                 |
      |                                |                                                                                                                                                                                                                                                              | Unit: byte            |                 |
      +--------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+-----------------+
      | auto.create.groups.enable      | Whether to automatically create consumer groups.                                                                                                                                                                                                             | true/false            | true            |
      |                                |                                                                                                                                                                                                                                                              |                       |                 |
      |                                | This parameter is not displayed on the console for some earlier instances. The function of automatically creating consumer groups is enabled by default and cannot be disabled on the console.                                                               |                       |                 |
      +--------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+-----------------+
      | max.connections.per.ip         | The maximum number of connections allowed from each IP address. Request for new connections will be rejected once the limit is reached.                                                                                                                      | 100-20,000            | 1000            |
      +--------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+-----------------+
      | unclean.leader.election.enable | Indicates whether to allow replicas not in the ISR set to be elected as the leader as a last resort, even though doing so may result in data loss.                                                                                                           | **true** or **false** | false           |
      +--------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+-----------------+
      | offsets.retention.minutes      | The longest period a consumption position can be retained starts from the time of submission. Positions retained beyond this duration will be deleted. Each time a consumption position is submitted to a topic partition, its retention period resets to 0. | 1440-30240            | 20160           |
      |                                |                                                                                                                                                                                                                                                              |                       |                 |
      |                                | This parameter is displayed as a static one for certain earlier instances.                                                                                                                                                                                   | Unit: minute          |                 |
      +--------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+-----------------+

   .. _kafka-ug-0007__table913673592919:

   .. table:: **Table 4** Static parameters (2.3.0/2.7/3.x instances)

      +--------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------+-----------------+
      | Parameter                      | Description                                                                                                                                                                          | Value Range       | Default Value   |
      +================================+======================================================================================================================================================================================+===================+=================+
      | connections.max.idle.ms        | Idle connection timeout (in ms). Connections that are idle for the duration specified by this parameter will be closed.                                                              | 5000-600,000      | 600,000         |
      |                                |                                                                                                                                                                                      |                   |                 |
      |                                |                                                                                                                                                                                      | Unit: millisecond |                 |
      +--------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------+-----------------+
      | log.retention.hours            | Maximum duration for storing log files.                                                                                                                                              | 1-168             | 72              |
      |                                |                                                                                                                                                                                      |                   |                 |
      |                                | This parameter takes effect only for topics that have no aging time configured. If there is aging time configured for topics, it overrides this parameter.                           | Unit: hour        |                 |
      +--------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------+-----------------+
      | group.max.session.timeout.ms   | Maximum session timeout for consumers. A longer timeout gives consumers more time to process messages between heartbeats but results in a longer time to detect failures.            | 6000-1,800,000    | 1,800,000       |
      |                                |                                                                                                                                                                                      |                   |                 |
      |                                |                                                                                                                                                                                      | Unit: millisecond |                 |
      +--------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------+-----------------+
      | default.replication.factor     | The default number of replicas configured for an automatically created topic.                                                                                                        | 1-3               | 3               |
      +--------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------+-----------------+
      | allow.everyone.if.no.acl.found | When this parameter is set to **true**, all users can access resources without ACL rules.                                                                                            | true/false        | true            |
      |                                |                                                                                                                                                                                      |                   |                 |
      |                                | This parameter is displayed only when is enabled for the instance or ciphertext access is used.                                                                                      |                   |                 |
      |                                |                                                                                                                                                                                      |                   |                 |
      |                                | This parameter of some earlier instances cannot be modified.                                                                                                                         |                   |                 |
      +--------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------+-----------------+
      | num.partitions                 | The default number of partitions configured for each automatically created topic.                                                                                                    | 1 ~ 200           | 3               |
      +--------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------+-----------------+
      | group.min.session.timeout.ms   | Minimum session timeout for consumers. A shorter timeout enables quicker failure detection but results in more frequent consumer heartbeating, which can overwhelm broker resources. | 6000-300,000      | 6000            |
      |                                |                                                                                                                                                                                      |                   |                 |
      |                                |                                                                                                                                                                                      | Unit: millisecond |                 |
      +--------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------+-----------------+

   .. note::

      -  To modify multiple dynamic or static parameters at a time, click **Modify** above the parameter list.
      -  If you want to restore the default values, click **Restore Default** in the row containing the desired parameter.

#. Click **Save**.

   .. note::

      Modifying dynamic parameters will not restart the instance. **Static parameter modification requires manual restart of the instance.**

.. |image1| image:: /_static/images/en-us_image_0143929918.png
