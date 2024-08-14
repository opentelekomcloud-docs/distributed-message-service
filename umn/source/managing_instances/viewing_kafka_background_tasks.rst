:original_name: kafka-ug-200119002.html

.. _kafka-ug-200119002:

Viewing Kafka Background Tasks
==============================

After you initiate certain instance operations listed in :ref:`Table 1 <kafka-ug-200119002__table135711125812>`, a background task will start for each operation. On the console, you can view the background task status and clear task information by deleting task records.

.. _kafka-ug-200119002__table135711125812:

.. table:: **Table 1** Backend task list

   +-----------------------------------+-----------------------------------------------------------+
   | Task Name                         | Description                                               |
   +===================================+===========================================================+
   | Creating an instance              | Creates a Kafka instance.                                 |
   +-----------------------------------+-----------------------------------------------------------+
   | Restart Instance                  | Restarts a Kafka instance.                                |
   +-----------------------------------+-----------------------------------------------------------+
   | Modifying Kafka parameters        | -  Modifies configuration parameters of Kafka.            |
   |                                   | -  Enables/Disables automatic topic creation.             |
   +-----------------------------------+-----------------------------------------------------------+
   | Change capacity threshold policy  | Changes capacity threshold policies for a Kafka instance. |
   +-----------------------------------+-----------------------------------------------------------+
   | Enabling or disabling SSL         | Switches between plaintext and ciphertext access.         |
   +-----------------------------------+-----------------------------------------------------------+
   | Configure public network access   | Enables/Disables public access.                           |
   +-----------------------------------+-----------------------------------------------------------+
   | Modify Specifications             | -  Expands the storage space.                             |
   |                                   | -  Adds brokers.                                          |
   |                                   | -  Increases the bandwidth.                               |
   |                                   | -  Increases the broker flavor.                           |
   +-----------------------------------+-----------------------------------------------------------+
   | Kafka partition reassignment      | Reassigns partitions of a topic.                          |
   +-----------------------------------+-----------------------------------------------------------+
   | Configure topic permission        | Grants permissions to users in a topic.                   |
   +-----------------------------------+-----------------------------------------------------------+

Procedure
---------

#. Log in to the console.

#. Click |image1| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click a Kafka instance to go to the **Basic Information** page.

#. In the navigation pane, choose **Background Tasks**.

#. On the **Background tasks** or **Scheduled tasks** tab page, click the time drop-down box, specify time, enter keywords in the search box, and press **Enter**. Tasks started in the specified time will be displayed.

   On the **Background Tasks** page, you can also perform the following operations:

   -  Click |image2| to refresh the task status.
   -  Click **Delete**. In the displayed **Delete Task** dialog box, click **OK** to clear the task information.

      .. note::

         You can delete a task only when it is in either of the following situations:

         -  The task is complete, which can be **Successful** or **Failed**.
         -  The task is **Canceled**.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
.. |image2| image:: /_static/images/en-us_image_0000001206335999.png
