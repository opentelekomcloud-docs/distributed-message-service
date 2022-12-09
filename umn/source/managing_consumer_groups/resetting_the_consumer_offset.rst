:original_name: kafka-ug-0014.html

.. _kafka-ug-0014:

Resetting the Consumer Offset
=============================

Resetting the consumer offset is to change the retrieval position of a consumer.

.. important::

   Messages may be retrieved more than once after the offset is reset. Exercise caution when performing this operation.

Prerequisites
-------------

The consumer offset cannot be reset on the fly. You must first stop retrieval of the desired consumer group.

Procedure
---------

#. Log in to the management console.

#. Click |image1| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click the desired Kafka instance to view the instance details.

#. In the navigation pane, choose the **Consumer Groups** tab.

#. Click the name of the desired consumer group.

#. On the **Consumer Offset** tab page, you can perform the following operations:

   -  To reset the consumer offset of all partitions of a topic, click **Reset Consumer Offset** in the row containing the desired topic.
   -  To reset the consumer offset of a single partition of a topic, click **Reset Consumer Offset** in the row containing the desired partition.

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
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------+
      | Time                              | Set this parameter if **Reset By** is set to **Time**.                                                                |
      |                                   |                                                                                                                       |
      |                                   | Select a time point. After the reset is complete, retrieval starts from this time point.                              |
      |                                   |                                                                                                                       |
      |                                   | -  **Earliest**: earliest offset                                                                                      |
      |                                   | -  **Custom Time Range**: a custom time point                                                                         |
      |                                   | -  **Latest**: latest offset                                                                                          |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------+
      | Offset                            | Set this parameter if **Reset By** is set to **Offset**.                                                              |
      |                                   |                                                                                                                       |
      |                                   | Enter an offset, which is greater than or equal to 0. After the reset is complete, retrieval starts from this offset. |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------+

#. Click **OK**.

#. Click **Yes** in the confirmation dialog box. The consumer offset is reset.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
