:original_name: kafka-ug-180604016.html

.. _kafka-ug-180604016:

Deleting Kafka Instances
========================

Scenario
--------

Delete one or more Kafka instances at a time on the DMS console.

.. important::

   Deleting a Kafka instance will delete the data in the instance without any backup. Exercise caution when performing this operation.

Prerequisites
-------------

The status of the Kafka instance you want to delete is **Running** or **Faulty**.


Deleting Kafka Instances
------------------------

#. Log in to the console.

#. Click |image1| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Delete pay-per-use Kafka instances in either of the following ways:

   -  Select one or more Kafka instances and click **Delete** in the upper left corner.
   -  In the row containing the Kafka instance to be deleted, choose **More** > **Delete**.
   -  Click the desired Kafka instance to view its details. In the upper right corner, choose **More** > **Delete**.

   .. note::

      Kafka instances in the **Creating**, **Changing**, **Change failed**, or **Restarting** state cannot be deleted.

#. In the **Delete Instance** dialog box, enter **DELETE** and click **OK** to delete the Kafka instance.

   It takes 1 to 60 seconds to delete a Kafka instance.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
