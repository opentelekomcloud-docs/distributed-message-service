:original_name: kafka-ug-0319001.html

.. _kafka-ug-0319001:

Configuring Public Access
=========================

To access a Kafka instance over a public network, enable public access and configure EIPs for the instance.

If you no longer need public access to the instance, you can disable it as required.

Procedure
---------

#. Log in to the management console.

#. Click |image1| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click a Kafka instance to go to the **Basic Information** tab page.

#. Configure public access.

   .. note::

      -  You can change the public access setting only when the Kafka instance is in the **Running** state.
      -  Only IPv4 EIPs can be bound to Kafka instances.

   **Enabling public access**

   Click |image2| next to **Public Access** to enable public access. For **Elastic IP Address**, select an EIP for each broker and then click |image3|.

   You can view the operation progress on the **Background Tasks** page. If the task status is **Successful**, the modification has succeeded.


   .. figure:: /_static/images/en-us_image_0000001329185932.png
      :alt: **Figure 1** Configuring public access

      **Figure 1** Configuring public access

   After public access is enabled, configure security group rules listed in :ref:`Table 1 <kafka-ug-0319001__table161395381402>` before attempting to access Kafka. For details about accessing Kafka, see :ref:`Accessing a Kafka Instance <kafka-ug190605003>`.

   .. _kafka-ug-0319001__table161395381402:

   .. table:: **Table 1** Security group rules

      +-----------+----------+------+-----------+-------------------------------------------------------------------+
      | Direction | Protocol | Port | Source    | Description                                                       |
      +===========+==========+======+===========+===================================================================+
      | Inbound   | TCP      | 9094 | 0.0.0.0/0 | Access Kafka through the public network (without SSL encryption). |
      +-----------+----------+------+-----------+-------------------------------------------------------------------+
      | Inbound   | TCP      | 9095 | 0.0.0.0/0 | Access Kafka through the public network (with SSL encryption).    |
      +-----------+----------+------+-----------+-------------------------------------------------------------------+

   **Disabling public access**

   Click |image4| next to **Public Access**.

   You can view the operation progress on the **Background Tasks** page. If the task status is **Successful**, the modification has succeeded.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
.. |image2| image:: /_static/images/en-us_image_0281104603.png
.. |image3| image:: /_static/images/en-us_image_0143920315.png
.. |image4| image:: /_static/images/en-us_image_0000001283221910.png
