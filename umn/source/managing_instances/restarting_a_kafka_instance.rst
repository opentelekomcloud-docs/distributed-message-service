:original_name: kafka-ug-180604015.html

.. _kafka-ug-180604015:

Restarting a Kafka Instance
===========================

You can restart one or more Kafka instances in batches on the DMS console.

Notes and Constraints
---------------------

-  When a Kafka instance is being restarted, message consumption and production requests of clients will be rejected.
-  To maintain service connections during instance restart, configure the retry mechanism on the client.

Prerequisite
------------

The status of the Kafka instance you want to restart is either **Running** or **Faulty**.

Procedure
---------

#. Log in to the console.

#. Click |image1| in the upper left corner to select the region where your instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Restart Kafka instances using one of the following methods:

   -  Select one or more Kafka instances and click **Restart** in the upper left corner.
   -  In the row containing the Kafka instance to be restarted, click **Restart**.
   -  Click the desired Kafka instance to go to the instance details page. In the upper right corner, click **Restart**.

#. In the **Restart Instance** dialog box, click **Yes** to restart the Kafka instance.

   It takes 3 to 15 minutes to restart a Kafka instance. After the instance is successfully restarted, its status should be **Running**.

   .. note::

      Restarting a Kafka instance only restarts the instance process and does not restart the VM where the instance is located.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
