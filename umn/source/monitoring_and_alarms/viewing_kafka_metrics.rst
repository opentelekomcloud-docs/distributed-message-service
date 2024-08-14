:original_name: kafka-ug-190605001.html

.. _kafka-ug-190605001:

Viewing Kafka Metrics
=====================

Cloud Eye monitors Kafka instance metrics in real time. You can view these metrics on the Cloud Eye console.

Prerequisites
-------------

At least one Kafka instance has been created. The instance has at least one available message.

Procedure
---------

#. Log in to the console.
#. Click |image1| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.
#. View the instance metrics in either of the following ways:

   -  In the row containing the desired instance, click **View Metric**. The Cloud Eye console is displayed. Click **By Instance**, **By Broker**, **By Topic**, **By Consumer Group**, or **By Smart Connect** to view monitoring data. The data is updated every minute.
   -  Click the desired Kafka instance to view its details. Choose **Monitoring**. The monitoring data can be viewed on the **By Instance**, **By Broker**, **By Topic**, **By Consumer Group**, and **By Smart Connect** tab pages. The data is updated every minute.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
