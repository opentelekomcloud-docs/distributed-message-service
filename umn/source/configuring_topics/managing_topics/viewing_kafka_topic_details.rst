:original_name: kafka_ug_0045.html

.. _kafka_ug_0045:

Viewing Kafka Topic Details
===========================

On the Kafka console, you can view basic information, partition and producer information, and subscriptions of a topic.

Procedure
---------

#. Log in to the console.

#. Click |image1| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click the desired Kafka instance to view its details.

#. In the navigation pane, choose **Topics**.

#. Click a topic to view its details.

   The general information, subscriptions, partitions, and producers are displayed.

   -  General information: topic name, brokers, partitions, and creation time

      .. note::

         -  For topics created much earlier, creation time is not displayed on the topic details page. See the console.
         -  For topics automatically created, and created by commands or code on the client, creation time is not displayed on the topic details page.

   -  Subscriptions: consumer group name and status, Coordinator (ID), and accumulated messages

      Click **Details** in the **Operation** column or the name of a consumer group.

      .. note::

         If an instance contains more than 10,000 consumer groups, the subscription relationships of topics cannot be queried.

   -  Partitions: partition No., minimum offset, maximum offset, number of messages, and message update time


      .. figure:: /_static/images/en-us_image_0000001756853218.png
         :alt: **Figure 1** Partitions

         **Figure 1** Partitions

   -  Producers: broker address, producer address, and producer connected time

      .. note::

         -  The producer information is displayed only when a producer is producing messages into topics.
         -  For topics created much earlier, **Producer** tab page is not displayed on the topic details page. See the console.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
