:original_name: kafka-ug-0004.html

.. _kafka-ug-0004:

Viewing Kafka Disk Usage
========================

This section describes how to view the disk usage of each broker on the Kafka console.

.. note::

   This function is unavailable for single-node instances.


Viewing Kafka Disk Usage
------------------------

#. Log in to the console.

#. Click |image1| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click a Kafka instance to go to the **Basic Information** page.

#. Go to the **Disk Usage Statistics** page.


   .. figure:: /_static/images/en-us_image_0000001377028284.png
      :alt: **Figure 1** Viewing disk usage

      **Figure 1** Viewing disk usage

   You can query topics that use the most disk space or topics that have used a specified amount or percentage of disk space.

   In the upper right corner of the page, click **View Metric**. On the displayed Cloud Eye page, you can view metrics of Kafka instances.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
