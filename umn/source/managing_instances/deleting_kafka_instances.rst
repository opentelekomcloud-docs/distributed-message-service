:original_name: kafka-ug-180604016.html

.. _kafka-ug-180604016:

Deleting Kafka Instances
========================

Delete one or more Kafka instances at a time on the DMS console.

Notes and Constraints
---------------------

Deleting a Kafka instance will clear the instance data without any backup. Exercise caution.

Prerequisites
-------------

The status of the Kafka instance you want to delete is **Running** or **Faulty**.

Procedure
---------

#. Log in to the console.

#. Click |image1| in the upper left corner to select the region where your instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Delete pay-per-use Kafka instances in either of the following ways:

   -  Select one or more Kafka instances and click **Delete** in the upper left corner.
   -  In the row containing the Kafka instance to be deleted, choose **More** > **Delete**.
   -  Click the desired Kafka instance to go to the instance details page. In the upper right corner, choose **More** > **Delete**.

#. In the **Delete Instance** dialog box, enter **DELETE** and click **OK** to delete the Kafka instance.

   It takes 1 to 60 seconds to delete a Kafka instance.

   The Kafka instances are deleted when they are no longer displayed in the instance list.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
