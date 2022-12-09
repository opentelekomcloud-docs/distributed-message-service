:original_name: kafka-ug-190904001.html

.. _kafka-ug-190904001:

Querying Messages
=================

Scenario
--------

You can view the offset of different partitions, the message size, creation time, and body of messages in topics.

Procedure
---------

#. Log in to the management console.

#. Click |image1| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click the desired Kafka instance to view the instance details.

#. Click the **Message Query** tab. Then specify the topic name, partition, and the search method.

   If no partition is specified, messages in all partitions of the topic are displayed.

   You can search by the following methods:

   -  **Creation time**: Search by the time that messages are created.
   -  **Offset**: Search by the message position.

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

#. (Optional) To restore the default settings, click **Reset**.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
