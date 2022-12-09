:original_name: kafka-ug-180604016.html

.. _kafka-ug-180604016:

Deleting an Instance
====================

Scenario
--------

On the DMS console, you can delete one or more Kafka instances that have been created or failed to be created.

.. important::

   Deleting a Kafka instance will delete the data in the instance without any backup. Exercise caution when performing this operation.

Prerequisites
-------------

The status of the Kafka instance you want to delete is **Running** or **Faulty**.

Deleting Kafka Instances
------------------------

#. Log in to the management console.

#. Click |image1| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Delete Kafka instances using one of the following methods:

   -  Select one or more Kafka instances and click **Delete** in the upper left corner.
   -  In the row containing the Kafka instance to be deleted, choose **More** > **Delete**.

   .. note::

      Kafka instances in the **Creating**, **Starting**, **Changing**, **Change failed**, or **Restarting** state cannot be deleted.

#. In the **Delete Instance** dialog box, click **Yes** to delete the Kafka instance.

   It takes 1 to 60 seconds to delete a Kafka instance.

Deleting Kafka Instances That Failed to Be Created
--------------------------------------------------

#. Log in to the management console.
#. Click |image2| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.
#. If there are Kafka instances that failed to be created, **Instance Creation Failures** and quantity information will be displayed.

   .. note::

      Instances that fail to be created do not occupy other resources.

#. Click **Instance Creation Failures** or the icon or quantity next to it.
#. Delete Kafka instances that failed to be created in either of the following ways:

   -  To delete all Kafka instances that failed to be created at once, click **Clear Failed Instance**.
   -  To delete a single Kafka instance that failed to be created, click **Delete** in the row containing the chosen Kafka instance.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
.. |image2| image:: /_static/images/en-us_image_0143929918.png
