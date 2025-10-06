:original_name: kafka_ug_0041.html

.. _kafka_ug_0041:

Disabling Smart Connect
=======================

Disable Smart Connect and resources can be freed.

Disabling Smart Connect does not affect services.

Notes and Constraints
---------------------

-  Brokers related to Smart Connect are automatically deleted.
-  If you disable Smart Connect and then enable it again, deleted Smart Connect tasks cannot be retrieved and need to be created again.
-  Unavailable for single-node instances.

Prerequisites
-------------

-  A Kafka instance has been created and is in the **Running** state.
-  :ref:`All Smart Connect tasks must be deleted <kafka_ug_0018__section2029318381532>`. This is to prevent running Smart Connect tasks from being lost after Smart Connect is disabled.

Procedure
---------

#. Log in to the console.

#. Click |image1| in the upper left corner to select the region where your instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Disable Smart Connect using either of the following methods:

   -  In the row containing the desired Kafka instance, choose **More** > **Disable Smart Connect**.
   -  Click the desired Kafka instance to go to the instance details page. Choose **More** > **Disable Smart Connect** in the upper right corner.

#. Click |image2| to disable Smart Connect. Then click **Next**.

#. Ensure that **Smart Connect** is disabled and click **Submit**.

   Smart Connect has been successfully disabled if the task is in the **Successful** state on the **Background Tasks** tab page of the **Background Tasks** page.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
.. |image2| image:: /_static/images/en-us_image_0000001283221910.png
