:original_name: kafka_ug_0045.html

.. _kafka_ug_0045:

Viewing Kafka Topic Details
===========================

On the Kafka console, you can view basic information, partition and producer information, and subscriptions of a topic.

Notes and Constraints
---------------------

-  If an instance contains more than 10,000 consumer groups, the subscribed topics cannot be queried.
-  The producer information is displayed only when a producer is producing messages into topics.

Procedure
---------

#. Log in to the console.

#. Click |image1| in the upper left corner to select the region where your instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click the desired instance to go to the instance details page.

#. In the navigation pane, choose **Topics**.

#. Click a topic to view its details.

   On the topic details page, the :ref:`basic information <kafka_ug_0045__table75960253133>`, :ref:`partitions <kafka_ug_0045__table3493841115917>`, :ref:`producers <kafka_ug_0045__table793651919179>`, and :ref:`subscriptions <kafka_ug_0045__table14692021153117>` are displayed.

   .. _kafka_ug_0045__table75960253133:

   .. table:: **Table 1** Basic topic information

      +-----------------------------------+------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                          |
      +===================================+======================================================================================================+
      | Topic Name                        | Name of this topic.                                                                                  |
      +-----------------------------------+------------------------------------------------------------------------------------------------------+
      | Brokers                           | This topic has been associated with brokers.                                                         |
      +-----------------------------------+------------------------------------------------------------------------------------------------------+
      | Partitions                        | Number of partitions of this topic.                                                                  |
      +-----------------------------------+------------------------------------------------------------------------------------------------------+
      | Created                           | .. caution::                                                                                         |
      |                                   |                                                                                                      |
      |                                   |    CAUTION:                                                                                          |
      |                                   |    The topic creation time is not displayed on the topic details page in any of the following cases: |
      |                                   |                                                                                                      |
      |                                   |    -  The topics were created much earlier. See the console.                                         |
      |                                   |    -  The topics were created automatically, or by commands or code on the client.                   |
      |                                   |                                                                                                      |
      |                                   | Time when this topic is created.                                                                     |
      +-----------------------------------+------------------------------------------------------------------------------------------------------+


   .. figure:: /_static/images/en-us_image_0000002309000337.png
      :alt: **Figure 1** Partitions

      **Figure 1** Partitions

   .. _kafka_ug_0045__table3493841115917:

   .. table:: **Table 2** Partition information of a topic

      ============== ========================================================
      Parameter      Description
      ============== ========================================================
      Partition      Partition No. of this topic.
      Minimum Offset Minimum offset of this partition.
      Maximum Offset Maximum offset of this partition.
      Messages       Number of messages in this partition.
      Updated        Time when the last message in this partition is updated.
      ============== ========================================================

   .. caution::

      For topics created much earlier, **Producer** tab page is not displayed on the topic details page. See the console.

   .. _kafka_ug_0045__table793651919179:

   .. table:: **Table 3** Producer information of a topic

      +--------------------+-----------------------------------------------------------------+
      | Parameter          | Description                                                     |
      +====================+=================================================================+
      | Broker Address     | Broker address of the Kafka instance connected to the producer. |
      +--------------------+-----------------------------------------------------------------+
      | Producer Address   | Address of the producer client.                                 |
      +--------------------+-----------------------------------------------------------------+
      | Producer Connected | Time when the producer is connected to the Kafka instance.      |
      +--------------------+-----------------------------------------------------------------+

   .. warning::

      If an instance contains more than 10,000 consumer groups, the subscribed topics cannot be queried.

   .. _kafka_ug_0045__table14692021153117:

   .. table:: **Table 4** Subscriptions of a topic

      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                   |
      +===================================+===============================================================================================================================+
      | Consumer Group Name               | Name of the consumer group that subscribes to this topic.                                                                     |
      |                                   |                                                                                                                               |
      |                                   | Clicking a consumer group name can go to the consumer group details page and view the consumer list and consumption progress. |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------+
      | Status                            | Current status of a consumer group.                                                                                           |
      |                                   |                                                                                                                               |
      |                                   | -  **DEAD**: The consumer group has no member or metadata.                                                                    |
      |                                   | -  **EMPTY**: The consumer group has metadata but has no member.                                                              |
      |                                   | -  **PREPARING_REBALANCE**: The consumer group is to be rebalanced.                                                           |
      |                                   | -  **COMPLETING_REBALANCE**: All members have joined the consumer group.                                                      |
      |                                   | -  **STABLE**: Members in the consumer group can consume messages normally.                                                   |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------+
      | Coordinator(ID)                   | Broker where the Coordinator component is.                                                                                    |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------+
      | Accumulated Messages              | Number of remaining messages that can be consumed in a consumer group.                                                        |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------+
      | Details                           | Clicking **Details** to go to the consumer group details.                                                                     |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------+

.. |image1| image:: /_static/images/en-us_image_0143929918.png
