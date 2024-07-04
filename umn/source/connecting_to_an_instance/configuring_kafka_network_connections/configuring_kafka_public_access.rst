:original_name: kafka-ug-0319001.html

.. _kafka-ug-0319001:

Configuring Kafka Public Access
===============================

To access a Kafka instance over a public network, enable public access and configure EIPs for the instance.

If you no longer need public access to the instance, you can disable it as required.

Prerequisites
-------------

-  You can change the public access setting only when the Kafka instance is in the **Running** state.
-  Kafka instances only support IPv4 EIPs. IPv6 EIPs are not supported.

Enabling Public Access
----------------------

#. Log in to the console.

#. Click |image1| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click a Kafka instance to go to the **Basic Information** page.

#. Click |image2| next to **Public Access** to enable public access. For **Elastic IP Address**, select an EIP for each broker. If the number of EIPs is insufficient, click **Create Elastic IP** to go to the **Create EIP** page and create EIPs. For details, see `Assigning an EIP <https://docs.otc.t-systems.com/en-us/usermanual/eip/eip_0002.html>`__. After the creation is complete, return to the page for enabling the public access. Click |image3| next to **Elastic IP Address**, select EIPs from the drop-down list. The number of EIPs must be the same as the number of brokers. Then click |image4| and the **Background Tasks** page is displayed.

   If the status of the task turns to **Successful**, public access is successfully enabled.


   .. figure:: /_static/images/en-us_image_0000001756508438.png
      :alt: **Figure 1** Enabling public access

      **Figure 1** Enabling public access

   After public access is enabled, configure the :ref:`access mode (plaintext or ciphertext) <kafka_ug_0044>` and security group rules listed in :ref:`Table 1 <kafka-ug-0319001__table8345121615136>` before attempting to access Kafka. For details about accessing Kafka, see :ref:`Connecting to an Instance <kafka-ug190605003>`.

   .. _kafka-ug-0319001__table8345121615136:

   .. table:: **Table 1** Security group rules

      +-----------+----------+------+-----------+-------------------------------------------------------+
      | Direction | Protocol | Port | Source    | Description                                           |
      +===========+==========+======+===========+=======================================================+
      | Inbound   | TCP      | 9094 | 0.0.0.0/0 | Accessing Kafka over a public network (in plaintext)  |
      +-----------+----------+------+-----------+-------------------------------------------------------+
      | Inbound   | TCP      | 9095 | 0.0.0.0/0 | Accessing Kafka over a public network (in ciphertext) |
      +-----------+----------+------+-----------+-------------------------------------------------------+

Disabling Public Access
-----------------------

#. Log in to the console.

#. Click |image5| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click a Kafka instance to go to the **Basic Information** page.

#. Before disabling public access, disable **Plaintext Access** and **Ciphertext Access** next to **Public Network Access**. Then click |image6| next to **Public Access**.

#. Click **OK**. The **Background Tasks** page is displayed. If the status of the task turns to **Successful**, public access is successfully disabled.

   After public access is disabled, configure security group rules listed in :ref:`Table 2 <kafka-ug-0319001__table19794123044119>` before attempting to access Kafka in a VPC. For details about accessing Kafka, see :ref:`Connecting to an Instance <kafka-ug190605003>`.

   .. _kafka-ug-0319001__table19794123044119:

   .. table:: **Table 2** Security group rules (private network access)

      +-----------+----------+------+-----------+--------------------------------------------------------------------------------+
      | Direction | Protocol | Port | Source    | Description                                                                    |
      +===========+==========+======+===========+================================================================================+
      | Inbound   | TCP      | 9092 | 0.0.0.0/0 | Accessing a Kafka instance over a private network within a VPC (in plaintext)  |
      +-----------+----------+------+-----------+--------------------------------------------------------------------------------+
      | Inbound   | TCP      | 9093 | 0.0.0.0/0 | Accessing a Kafka instance over a private network within a VPC (in ciphertext) |
      +-----------+----------+------+-----------+--------------------------------------------------------------------------------+

   .. note::

      After a security group is created, its default inbound rule allows communication among ECSs within the security group and its default outbound rule allows all outbound traffic. In this case, you can access a Kafka instance within a VPC, and do not need to add rules according to :ref:`Table 2 <kafka-ug-0319001__table19794123044119>`.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
.. |image2| image:: /_static/images/en-us_image_0000001605213324.png
.. |image3| image:: /_static/images/en-us_image_0000001540501562.png
.. |image4| image:: /_static/images/en-us_image_0000001654533309.png
.. |image5| image:: /_static/images/en-us_image_0143929918.png
.. |image6| image:: /_static/images/en-us_image_0000001605533602.png
