:original_name: kafka_ug_0046.html

.. _kafka_ug_0046:

Deleting Kafka Messages
=======================

This section describes how to delete messages stored in a topic on the console.

.. important::

   Deleted messages cannot be recovered.

Prerequisites
-------------

Before deleting a message, set the **auto.offset.reset** parameter in the code of consumption. **auto.offset.reset** specifies the consumption policy of a consumer when there is no initial offset in Kafka or the current offset does not exist (for example, the current offset has been deleted). Options:

-  **latest**: The offset is automatically reset to the latest offset.
-  **earliest**: The offset is automatically reset to the earliest offset.
-  **none**: The system throws an exception to the consumer.

.. important::

   If this parameter is set to **latest**, the producer may start to send messages to new partitions (if any) before the consumer resets to the initial offset. As a result, some messages will be lost.

Procedure
---------

#. Log in to the console.

#. Click |image1| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click the desired Kafka instance to view its details.

#. In the navigation pane, choose **Topics**.

#. Perform either of the following steps to display the **Delete Message** dialog box:

   -  If ciphertext access has not been enabled for the instance, click **Delete Messages** in the row that contains the topic whose messages you want to delete.
   -  If ciphertext access has been enabled for the instance, choose **More** > **Delete Messages** in the row that contains the topic whose messages you want to delete.

#. Set the parameters for deleting messages, as shown in :ref:`Table 1 <kafka_ug_0046__table10182314115320>`.


   .. figure:: /_static/images/en-us_image_0000002065181241.png
      :alt: **Figure 1** Deleting messages

      **Figure 1** Deleting messages

   .. _kafka_ug_0046__table10182314115320:

   .. table:: **Table 1** Parameters for deleting a message

      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                                     |
      +===================================+=================================================================================================================================================================================================================================+
      | Partition                         | Select the ID of the partition where the message is located.                                                                                                                                                                    |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Offset                            | Enter an offset. The data after the earliest offset and before this offset will be deleted. For example, if the earliest offset is 2 and the entered offset is 5, the messages whose offset ranges from 2 to 4 will be deleted. |
      |                                   |                                                                                                                                                                                                                                 |
      |                                   | .. note::                                                                                                                                                                                                                       |
      |                                   |                                                                                                                                                                                                                                 |
      |                                   |    -  If **Offset** is set to **-1**, all messages in the partition will be deleted.                                                                                                                                            |
      |                                   |    -  If the offset you entered is not between the earliest offset and the latest offset of the specified partition, no messages will be deleted.                                                                               |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   To delete messages from multiple partitions, click **Add Partition** and specify the partition and offset for the messages to be deleted. 10 partitions can be deleted at most at a time.

#. Click **OK**. The **Deletion Result** dialog box is displayed. Click **OK** to delete the messages.


   .. figure:: /_static/images/en-us_image_0000001803937277.png
      :alt: **Figure 2** Deletion result

      **Figure 2** Deletion result

.. |image1| image:: /_static/images/en-us_image_0143929918.png
