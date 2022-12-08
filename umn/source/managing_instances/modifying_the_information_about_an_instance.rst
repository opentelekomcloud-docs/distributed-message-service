:original_name: kafka-ug-180604017.html

.. _kafka-ug-180604017:

Modifying the Information About an Instance
===========================================

After creating a Kafka instance, you can modify some parameters of the instance based on service requirements, including the instance name, description, security group, and capacity threshold policy.

Procedure
---------

#. Log in to the management console.

#. Click |image1| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click the desired Kafka instance to view the instance details.

#. Modify the following parameters if needed:

   -  Instance Name
   -  Description
   -  Security Group
   -  Public Access (For details about how to change the public access configuration, see :ref:`Configuring Public Access <kafka-ug-0319001>`.)
   -  Capacity Threshold Policy (Modifying this setting will not restart the instance.)
   -  Automatic Topic Creation (Modifying this setting will restart the instance.)

   After the parameters are modified, view the modification result in one of the following ways:

   -  If **Capacity Threshold Policy**, **Public Access**, or **Automatic Topic Creation** has been modified, you will be redirected to the **Background Tasks** page, which displays the modification progress and result.
   -  If **Instance Name**, **Description**, or **Security Group** has been modified, the modification result will be displayed on the upper right corner of the page.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
