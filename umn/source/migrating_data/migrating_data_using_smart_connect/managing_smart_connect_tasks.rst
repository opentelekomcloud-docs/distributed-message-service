:original_name: kafka_ug_0018.html

.. _kafka_ug_0018:

Managing Smart Connect Tasks
============================

View, delete, start, pause, or restart a Smart Connect task.

.. note::

   This function is unavailable for single-node instances.

Prerequisites
-------------

A Smart Connect task has been :ref:`created <kafka-ug-0034>`.

Viewing Smart Connect Tasks
---------------------------

#. Log in to the management console.
#. Click |image1| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.
#. Click the desired Kafka instance to view its details.
#. In the navigation pane, choose **Smart Connect**.
#. Click a Smart Connect task name to go to the details page.
#. View the basic information, source, and target of the Smart Connect task.

   .. note::

      The source and target are displayed on the task details page only when they have been configured for the Smart Connect task.

.. _kafka_ug_0018__section2029318381532:

Deleting a Smart Connect Task
-----------------------------

#. Log in to the management console.
#. Click |image2| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.
#. Click the desired Kafka instance to view its details.
#. In the navigation pane, choose **Smart Connect**.
#. In the row containing the Smart Connect task to be deleted, click **Delete**.
#. Click **OK**.

Starting or Pausing a Smart Connect Task
----------------------------------------

After a task of a Kafka instance is paused, data of the instance will not be synchronized to another Kafka instance or other cloud services.

#. Log in to the console.
#. Click |image3| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.
#. Click the desired Kafka instance to view its details.
#. In the navigation pane, choose **Smart Connect**.
#. Perform the required operation:

   -  To start a Smart Connect task, click **Start** in the row that contains the task.
   -  To pause a Smart Connect task, click **Pause** in the row containing the task, then click **OK** in the dialog box that is displayed.

Restarting a Smart Connect Task
-------------------------------

#. Log in to the console.

#. Click |image4| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click the desired Kafka instance to view its details.

#. In the navigation pane, choose **Smart Connect**.

#. In the row containing the desired Smart Connect task, click **Restart**.

   .. important::

      -  Modifying the source or target parameters after a Smart Connect task is created may cause the restart to fail.
      -  Restarting a Smart Connect task resets the synchronization progress and the synchronization task will be restarted.

#. Click **OK**.

   Once the task is restarted, a success message is displayed in the upper left area of the page.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
.. |image2| image:: /_static/images/en-us_image_0143929918.png
.. |image3| image:: /_static/images/en-us_image_0143929918.png
.. |image4| image:: /_static/images/en-us_image_0143929918.png
