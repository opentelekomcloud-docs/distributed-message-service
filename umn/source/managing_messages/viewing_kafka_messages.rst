:original_name: kafka-ug-190904001.html

.. _kafka-ug-190904001:

Viewing Kafka Messages
======================

Scenario
--------

You can view the offset of different partitions, the message size, creation time, and body of messages in topics.


Viewing Kafka Messages
----------------------

#. Log in to the console.

#. Click |image1| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click the desired Kafka instance to view its details.

#. In the left navigation pane, choose **Message Query**.

#. Set the query parameters by referring to :ref:`Table 1 <kafka-ug-190904001__table37671048101019>`.

   .. _kafka-ug-190904001__table37671048101019:

   .. table:: **Table 1** Message query parameters

      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                                                    |
      +===================================+================================================================================================================================================================================================================================================+
      | Topic Name                        | Name of the topic to be queried.                                                                                                                                                                                                               |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Partition                         | Partition where the messages are located.                                                                                                                                                                                                      |
      |                                   |                                                                                                                                                                                                                                                |
      |                                   | If no partition is specified, messages in all partitions of the topic are displayed in the query result.                                                                                                                                       |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Search By                         | The following methods are supported:                                                                                                                                                                                                           |
      |                                   |                                                                                                                                                                                                                                                |
      |                                   | -  **Creation time**: Search by the time that messages are created.                                                                                                                                                                            |
      |                                   | -  **Offset**: Search by the message position.                                                                                                                                                                                                 |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Search For                        | This parameter is displayed only when **Search By** is set to **Creation time**.                                                                                                                                                               |
      |                                   |                                                                                                                                                                                                                                                |
      |                                   | Enter a keyword in the message body.                                                                                                                                                                                                           |
      |                                   |                                                                                                                                                                                                                                                |
      |                                   | .. note::                                                                                                                                                                                                                                      |
      |                                   |                                                                                                                                                                                                                                                |
      |                                   |    Due to resource and performance restrictions, query with content is limited to 10 results. Each search covers at most 10,000 records, or 200 MB. For large records (> 20 KB per message) or a long period, dump messages for offline query. |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   .. note::

      If a topic contains a large amount of data, an internal service error may be reported when you query messages in a topic with only one replica. You can shorten the time range for query based on the data volume.

#. Click **Search** to query messages.

   Parameter description:

   -  **Topic Name**: name of the topic where the message is located
   -  **Partition**: partition where the message is located
   -  **Offset**: position of the message in the partition
   -  **Message Size (Byte)** size of the message
   -  **Created**: time when the message is created. The message creation time is specified by **CreateTime** when a producer creates messages. If this parameter is not set during message creation, the message creation time is year 1970 by default.

#. Click **View Message Body**. In the displayed **View Message Body** dialog box, view the message content, including the topic name, partition, offset, creation time, and message body.

   .. note::

      The console displays messages smaller than 4 KB. To view messages larger than 4 KB, click **Download Message**.

#. (Optional) To restore the default settings, click **Reset**.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
