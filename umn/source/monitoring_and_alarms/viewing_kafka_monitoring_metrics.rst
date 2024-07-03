:original_name: kafka-ug-190605001.html

.. _kafka-ug-190605001:

Viewing Kafka Monitoring Metrics
================================

Scenario
--------

Cloud Eye monitors Kafka instance metrics in real time. You can view these metrics on the Cloud Eye console.

Prerequisites
-------------

At least one Kafka instance has been created. The instance has at least one available message.


Viewing Kafka Monitoring Metrics
--------------------------------

#. Log in to the console.
#. Click |image1| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.
#. View the instance metrics in either of the following ways:

   -  In the row containing the desired instance, click **View Metric**. On the Cloud Eye console, view the metrics of the instance, brokers, topics, and consumer groups. Metric data is reported to Cloud Eye every minute.
   -  Click the desired Kafka instance to view its details. In the navigation pane, choose **Monitoring** view. On the displayed page, view the metrics of the instance, brokers, topics, and consumer groups. Metric data is reported to Cloud Eye every minute.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
