:original_name: kafka-ug-190605001.html

.. _kafka-ug-190605001:

Viewing Kafka Metrics
=====================

Cloud Eye monitors Kafka instance metrics in real time. You can view these metrics on the Cloud Eye console.

Prerequisite
------------

At least one Kafka instance has been created. The instance has at least one available message.

Procedure
---------

#. Log in to the console.

#. Click |image1| in the upper left corner to select the region where your instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. View the instance metrics in either of the following ways:

   -  In the row containing the desired instance, click **View Metric**. On the Cloud Eye console, view the metrics. Metric data is reported to Cloud Eye every minute.
   -  Click the desired instance to go to the instance details page. In the navigation pane, choose **Monitoring**. On the displayed page, view the monitoring data. The data is updated every minute.

   Click the following dimensions to view monitoring data:

   -  Single-node instance: **By Instance**, **By Broker**, **By Topic**, or **By Consumer Group**.
   -  Cluster instance: **By Instance**, **By Broker**, **By Topic**, **By Consumer Group**, or **By Smart Connect**.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
