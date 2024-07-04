:original_name: kafka-ug-0014.html

.. _kafka-ug-0014:

Viewing and Resetting Kafka Consumption Offsets
===============================================

This section describes how to view and reset consumption offsets. Resetting consumption offsets is to change the consumption position for consumers.

.. important::

   Messages may be retrieved more than once after the offset is reset. Exercise caution when performing this operation.

Prerequisites
-------------

The consumer offset cannot be reset on the fly. You must first stop retrieval of the desired consumer group.

.. important::

   After a client is stopped, the server considers the client offline only after the time period specified in **ConsumerConfig.SESSION_TIMEOUT_MS_CONFIG** (1000 ms by default).

Viewing Consumer Offsets (Console)
----------------------------------

#. Log in to the console.
#. Click |image1| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.
#. Click the desired Kafka instance to view the instance details.
#. In the navigation pane, choose **Consumer Groups**.
#. Click the name of the desired consumer group.
#. On the **Consumer Offset** tab page, view the list of topics that the consumer group has subscribed to, total number of messages accumulated in the topic, message consumption progress in each partition of the topic (accumulated messages, offset, latest offset, consumer ID, consumer address, and client ID).
#. (Optional) To query the consumer offsets of a specific topic, enter the topic name in the search box and press **Enter**.

Viewing Consumer Offsets (Kafka CLI)
------------------------------------

-  For a Kafka instance with ciphertext access disabled, run the following command in the **/bin** directory of the Kafka client:

   .. code-block::

      ./kafka-consumer-groups.sh --bootstrap-server ${connection-address} --offsets --describe --all-groups

-  For a Kafka instance with ciphertext access enabled, do as follows:

   #. (Optional) For the Kafka security protocol, is SASL_PLAINTEXT or SASL_SSL used?

      -  SASL_PLAINTEXT: Skip this step if the username and password are already set. In other cases, create the **ssl-user-config.properties** file in the **/config** directory of the Kafka client. Add the username and password by referring to :ref:`3 <kafka-ug-180801001__li5414277457>`.
      -  SASL_SSL: Skip this step if the username, password, and SSL certificate are already set. In other cases, create the **ssl-user-config.properties** file in the **/config** directory of the Kafka client. Add the username and password, and the SSL certificate configuration by referring to :ref:`3 <kafka-ug-180801001__li5414277457>`.

   #. Run the following command in the **/bin** directory of the Kafka client:

      .. code-block::

         ./kafka-consumer-groups.sh --bootstrap-server ${connection-address} --offsets --describe --all-groups --command-config ./config/ssl-user-config.properties

Resetting Consumer Offsets
--------------------------

#. Log in to the console.

#. Click |image2| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click the desired Kafka instance to view the instance details.

#. In the navigation pane, choose the **Consumer Groups** tab.

#. Click the name of the desired consumer group.

#. On the **Consumer Offset** tab page, you can perform the following operations:

   -  To reset the consumer offset of all partitions of a single topic, click **Reset Consumer Offset** in the row containing the desired topic.
   -  To reset the consumer offset of a single partition of a single topic, click **Reset Consumer Offset** in the row containing the desired partition.
   -  To reset the consumer offset of all partitions in all topics, click **One-touch Reset Consumer Offset** above the list.

#. In the displayed **Reset Consumer Offset** dialog box, set the parameters by referring to :ref:`Table 1 <kafka-ug-0014__table13921162119239>`.

   .. _kafka-ug-0014__table13921162119239:

   .. table:: **Table 1** Parameters for resetting the consumer offset

      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                           |
      +===================================+=======================================================================================================================+
      | Reset By                          | You can reset an offset by:                                                                                           |
      |                                   |                                                                                                                       |
      |                                   | -  Time: Reset the offset to the specified time.                                                                      |
      |                                   | -  Offset: Reset the offset to the specified position.                                                                |
      |                                   |                                                                                                                       |
      |                                   | If you reset offsets in batches, they can only be reset to the specified time.                                        |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------+
      | Time                              | Set this parameter if **Reset By** is set to **Time**.                                                                |
      |                                   |                                                                                                                       |
      |                                   | Select a time point. After the reset is complete, retrieval starts from this time point.                              |
      |                                   |                                                                                                                       |
      |                                   | -  **Earliest**: earliest offset                                                                                      |
      |                                   | -  **Custom**: a custom time point                                                                                    |
      |                                   | -  **Latest**: latest offset                                                                                          |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------+
      | Offset                            | Set this parameter if **Reset By** is set to **Offset**.                                                              |
      |                                   |                                                                                                                       |
      |                                   | Enter an offset, which is greater than or equal to 0. After the reset is complete, retrieval starts from this offset. |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------+

#. Click **OK**.

#. Click **Yes** in the confirmation dialog box. The consumer offset is reset.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
.. |image2| image:: /_static/images/en-us_image_0143929918.png
