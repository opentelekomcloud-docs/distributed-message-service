:original_name: kafka-ug-200119002.html

.. _kafka-ug-200119002:

Viewing Background Tasks
========================

After you initiate certain instance operations such as configuring public access and modifying the capacity threshold policy, a background task will start for each operation. On the console, you can view the background task status and clear task information by deleting task records.

Procedure
---------

#. Log in to the management console.

#. Click |image1| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click a Kafka instance to go to the **Basic Information** tab page.

#. Click the **Background Tasks** tab.

   A list of background tasks is displayed.

#. In the upper right corner, click the time period next to the calendar icon, select the start time and end time, and click **OK**. Tasks started in the specified period are displayed.

   On the **Background Tasks** page, you can also perform the following operations:

   -  Click |image2| to refresh the task status.
   -  Click **Delete**. In the displayed **Delete Task** dialog box, click **Yes** to clear the task information.

      .. note::

         You can only delete the records of tasks in the **Successful** or **Failed** state.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
.. |image2| image:: /_static/images/en-us_image_0000001206335999.png
