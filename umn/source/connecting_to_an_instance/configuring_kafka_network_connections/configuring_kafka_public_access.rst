:original_name: kafka-ug-0319001.html

.. _kafka-ug-0319001:

Configuring Kafka Public Access
===============================

Clients can use IPv4 or IPv6 addresses to access a Kafka instance over a public network.

-  By IPv4: On the Kafka console, enable public access and configure EIPs for the instance.
-  By IPv6: Enable IPv6 in Kafka instance creation and add IPv6 addresses to the shared bandwidth to support both private and public IPv6 access.

On the Kafka console, the procedures for configuring public IPv4 access vary depending on the content displayed in the **Connection** area on the **Basic Information** page.

-  When IPv6 is disabled, refer to :ref:`Enabling Public IPv4 Access (Plaintext or Ciphertext Access Can Be Changed) <kafka-ug-0319001__section834421617132>` and :ref:`Disabling Public IPv4 Access (Plaintext or Ciphertext Access Can Be Changed) <kafka-ug-0319001__section13340025121318>`.
-  When IPv6 is enabled, refer to :ref:`Enabling Public IPv4 Access (SASL Cannot Be Changed) <kafka-ug-0319001__section7716364362>` and :ref:`Disabling Public IPv4 Access (SASL Cannot Be Changed) <kafka-ug-0319001__section1992287141316>`.

Prerequisites
-------------

-  You can change the public access setting only when the Kafka instance is in the **Running** state.
-  (Optional) To access a Kafka instance using IPv6 addresses, ensure that IPv6 is enabled for the Kafka instance.

Notes and Constraints
---------------------

Kafka instances only support IPv4 EIPs. IPv6 EIPs are not supported.

.. _kafka-ug-0319001__section7716364362:

Enabling Public IPv4 Access (SASL Cannot Be Changed)
----------------------------------------------------

#. Log in to the console.

#. Click |image1| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click a Kafka instance to go to the **Basic Information** page.

#. Click |image2| next to **Public Access** to enable public access. For **Elastic IP Address**, select an EIP for each broker.

   If the EIPs are insufficient, do as follows to set them.

   a. Click **Create Elastic IP** to go to the **Create EIP** page and create EIPs. For details, see `Assigning an EIP <https://docs.otc.t-systems.com/en-us/usermanual/eip/eip_0002.html>`__
   b. After the creation is complete, return to the public access enabling page.
   c. Click |image3| after **Elastic IP Address**, select an EIP for each broker and then click |image4|.
   d. You can view the operation progress on the **Background Tasks** page. If the task status is **Successful**, the modification has succeeded.

   After public access is enabled, configure security group rules listed in :ref:`Table 1 <kafka-ug-0319001__table161395381402>` before attempting to access Kafka. For details about accessing Kafka, see :ref:`Connecting to an Instance <kafka-ug190605003>`.

   .. _kafka-ug-0319001__table161395381402:

   .. table:: **Table 1** Kafka instance security group rules (public IPv4 access)

      +-----------+----------+------+------+-----------+-----------------------------------------------------+
      | Direction | Protocol | Type | Port | Source    | Description                                         |
      +===========+==========+======+======+===========+=====================================================+
      | Inbound   | TCP      | IPv4 | 9094 | 0.0.0.0/0 | Accessing Kafka over a public network (without SSL) |
      +-----------+----------+------+------+-----------+-----------------------------------------------------+
      | Inbound   | TCP      | IPv4 | 9095 | 0.0.0.0/0 | Accessing Kafka over a public network (with SSL)    |
      +-----------+----------+------+------+-----------+-----------------------------------------------------+

.. _kafka-ug-0319001__section1992287141316:

Disabling Public IPv4 Access (SASL Cannot Be Changed)
-----------------------------------------------------

#. Log in to the console.

#. Click |image5| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click a Kafka instance to go to the **Basic Information** page.

#. Click |image6| next to **Public Access**.

   You can view the operation progress on the **Background Tasks** page. If the task status is **Successful**, the modification has succeeded.

   After public access is disabled, configure security group rules listed in :ref:`Table 2 <kafka-ug-0319001__table5171161201316>` before attempting to access Kafka in a VPC. For details about accessing Kafka, see :ref:`Connecting to an Instance <kafka-ug190605003>`.

   .. _kafka-ug-0319001__table5171161201316:

   .. table:: **Table 2** Kafka instance security group rules (private access)

      +-----------+----------+------+------+-----------+------------------------------------------------------------------------------+
      | Direction | Protocol | Type | Port | Source    | Description                                                                  |
      +===========+==========+======+======+===========+==============================================================================+
      | Inbound   | TCP      | IPv4 | 9092 | 0.0.0.0/0 | Accessing a Kafka instance over a private network within a VPC (without SSL) |
      +-----------+----------+------+------+-----------+------------------------------------------------------------------------------+
      | Inbound   | TCP      | IPv4 | 9093 | 0.0.0.0/0 | Accessing a Kafka instance over a private network within a VPC (with SSL)    |
      +-----------+----------+------+------+-----------+------------------------------------------------------------------------------+

   .. note::

      After a security group is created, its default inbound rule allows communication among ECSs within the security group and its default outbound rule allows all outbound traffic. In this case, you can access a Kafka instance within a VPC, and do not need to add rules according to :ref:`Table 2 <kafka-ug-0319001__table5171161201316>`.

.. _kafka-ug-0319001__section834421617132:

Enabling Public IPv4 Access (Plaintext or Ciphertext Access Can Be Changed)
---------------------------------------------------------------------------

#. Log in to the console.

#. Click |image7| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click a Kafka instance to go to the **Basic Information** page.

#. Click |image8| next to **Public Access** to enable public access. For **Elastic IP Address**, select an EIP for each broker.

   If the EIPs are insufficient, do as follows to set them.

   a. Click **Create Elastic IP** to go to the **Create EIP** page and create EIPs. For details, see `Assigning an EIP <https://docs.otc.t-systems.com/en-us/usermanual/eip/eip_0002.html>`__
   b. After the creation is complete, return to the public access enabling page.
   c. Click |image9| after **Elastic IP Address**, select an EIP for each broker and then click |image10|. The **Background Tasks** page is displayed.
   d. If the status of the task turns to **Successful**, public access is successfully enabled.


   .. figure:: /_static/images/en-us_image_0000001756508438.png
      :alt: **Figure 1** Enabling public access

      **Figure 1** Enabling public access

   After public access is enabled, configure the :ref:`access mode (plaintext or ciphertext) <kafka_ug_0044>` and security group rules listed in :ref:`Table 3 <kafka-ug-0319001__table8345121615136>` before attempting to access Kafka. For details about accessing Kafka, see :ref:`Connecting to an Instance <kafka-ug190605003>`.

   .. _kafka-ug-0319001__table8345121615136:

   .. table:: **Table 3** Kafka instance security group rules (public IPv4 access)

      ========= ======== ==== ==== ========= =================================
      Direction Protocol Type Port Source    Description
      ========= ======== ==== ==== ========= =================================
      Inbound   TCP      IPv4 9094 0.0.0.0/0 Public plaintext access to Kafka
      Inbound   TCP      IPv4 9095 0.0.0.0/0 Public ciphertext access to Kafka
      ========= ======== ==== ==== ========= =================================

.. _kafka-ug-0319001__section13340025121318:

Disabling Public IPv4 Access (Plaintext or Ciphertext Access Can Be Changed)
----------------------------------------------------------------------------

#. Log in to the console.

#. Click |image11| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click a Kafka instance to go to the **Basic Information** page.

#. Before disabling public access, disable **Plaintext Access** and **Ciphertext Access** next to **Public Network Access**. Then click |image12| next to **Public Access**.

#. Click **OK**. The **Background Tasks** page is displayed. If the status of the task turns to **Successful**, public access is successfully disabled.

   After public access is disabled, configure security group rules listed in :ref:`Table 4 <kafka-ug-0319001__table19794123044119>` before attempting to access Kafka in a VPC. For details about accessing Kafka, see :ref:`Connecting to an Instance <kafka-ug190605003>`.

   .. _kafka-ug-0319001__table19794123044119:

   .. table:: **Table 4** Kafka instance security group rules (private access)

      +-----------+----------+------+------+-----------+--------------------------------------------------------------------------------+
      | Direction | Protocol | Type | Port | Source    | Description                                                                    |
      +===========+==========+======+======+===========+================================================================================+
      | Inbound   | TCP      | IPv4 | 9092 | 0.0.0.0/0 | Accessing a Kafka instance over a private network within a VPC (in plaintext)  |
      +-----------+----------+------+------+-----------+--------------------------------------------------------------------------------+
      | Inbound   | TCP      | IPv4 | 9093 | 0.0.0.0/0 | Accessing a Kafka instance over a private network within a VPC (in ciphertext) |
      +-----------+----------+------+------+-----------+--------------------------------------------------------------------------------+

   .. note::

      After a security group is created, its default inbound rule allows communication among ECSs within the security group and its default outbound rule allows all outbound traffic. In this case, you can access a Kafka instance within a VPC, and do not need to add rules according to :ref:`Table 4 <kafka-ug-0319001__table19794123044119>`.

Enabling IPv6 Public Network Access
-----------------------------------

#. Log in to the console.

#. Click |image13| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click a Kafka instance to go to the **Basic Information** page.

#. .. _kafka-ug-0319001__li1128073022615:

   In the **Connection** area, obtain IPv6 **Instance Address (Private Network)**. In the **Network** area, view and record the VPC and subnet.

#. Click |image14| in the upper left corner of the management console and choose **Network** > **Elastic IP**. The **EIPs** page is displayed.

#. Choose **Shared Bandwidths** in the navigation pane.

#. Apply for a shared bandwidth. For details, see `Assigning a Shared Bandwidth <https://docs.otc.t-systems.com/en-us/usermanual/eip/bandwidth_0003.html>`__.

   If a shared bandwidth already exists, you do not need to apply for one again.

#. In the row containing the shared bandwidth, click **Add Public IP Address**.

#. Set the parameters as described in :ref:`Table 5 <kafka-ug-0319001__table05781342607>` and click **OK**.

   .. _kafka-ug-0319001__table05781342607:

   .. table:: **Table 5** Adding public IP parameters

      +-------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter         | Description                                                                                                                                                           |
      +===================+=======================================================================================================================================================================+
      | Public IP Address | Select **IPv6 Address**.                                                                                                                                              |
      +-------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | VPC               | Select the VPC in :ref:`5 <kafka-ug-0319001__li1128073022615>` from the drop-down list.                                                                               |
      +-------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Subnet            | Select the subnet in :ref:`5 <kafka-ug-0319001__li1128073022615>` from the drop-down list. Select all IPv6 addresses in :ref:`5 <kafka-ug-0319001__li1128073022615>`. |
      +-------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. After the shared bandwidth is configured, set a Kafka instance security group with the rules described in :ref:`Table 6 <kafka-ug-0319001__table136445264129>`.

   .. _kafka-ug-0319001__table136445264129:

   .. table:: **Table 6** Kafka instance security group rules (IPv6 access)

      +-----------+----------+------+------+--------+--------------------------------------------------------------------------+
      | Direction | Protocol | Type | Port | Source | Description                                                              |
      +===========+==========+======+======+========+==========================================================================+
      | Inbound   | TCP      | IPv6 | 9192 | ::/0   | Accessing a Kafka instance using IPv6 addresses (without SSL encryption) |
      +-----------+----------+------+------+--------+--------------------------------------------------------------------------+
      | Inbound   | TCP      | IPv6 | 9193 | ::/0   | Accessing a Kafka instance using IPv6 addresses (with SSL encryption)    |
      +-----------+----------+------+------+--------+--------------------------------------------------------------------------+

   .. note::

      -  When a client is connected to a Kafka instance over an IPv6 public network, the Kafka connection addresses are the IPv6 addresses in **Instance Address (Private Network)**.
      -  To access a Kafka instance over an IPv6 public network, add the client NIC to the shared bandwidth. Shared bandwidths are using a connected network. The shared bandwidth of the client NIC and that of the Kafka instance can be different.

Disabling IPv6 Public Access
----------------------------

Remove the IPv6 addresses of a Kafka instance from the shared bandwidth. For details, see `Removing EIPs from a Shared Bandwidth <https://docs.otc.t-systems.com/en-us/usermanual/eip/bandwidth_0005.html>`__.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
.. |image2| image:: /_static/images/en-us_image_0281104603.png
.. |image3| image:: /_static/images/en-us_image_0000001540501562.png
.. |image4| image:: /_static/images/en-us_image_0143920315.png
.. |image5| image:: /_static/images/en-us_image_0143929918.png
.. |image6| image:: /_static/images/en-us_image_0000001654533317.png
.. |image7| image:: /_static/images/en-us_image_0143929918.png
.. |image8| image:: /_static/images/en-us_image_0000001191767177.png
.. |image9| image:: /_static/images/en-us_image_0000001540501562.png
.. |image10| image:: /_static/images/en-us_image_0000001191769789.png
.. |image11| image:: /_static/images/en-us_image_0143929918.png
.. |image12| image:: /_static/images/en-us_image_0000001605533602.png
.. |image13| image:: /_static/images/en-us_image_0143929918.png
.. |image14| image:: /_static/images/en-us_image_0000001143589128.png
