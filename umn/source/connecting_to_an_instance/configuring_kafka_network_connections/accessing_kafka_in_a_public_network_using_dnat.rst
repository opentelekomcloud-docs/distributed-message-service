:original_name: kafka-dnat.html

.. _kafka-dnat:

Accessing Kafka in a Public Network Using DNAT
==============================================

Enable public access in either of the following ways:

-  On the Kafka console, access Kafka instances using EIPs. For details, see :ref:`Configuring Kafka Public Access <kafka-ug-0319001>`.
-  Configure port mapping from EIPs to specified instance ports using destination NAT (DNAT).

This section describes how to access Kafka over a public network using DNAT.

Prerequisites
-------------

You have created EIPs. The number of EIPs is the same as the number of brokers in the Kafka instance. For details about how to create an EIP, see `Assigning an EIP <https://docs.otc.t-systems.com/en-us/usermanual/eip/eip_0002.html>`__.

Step 1: Obtain Information About the Kafka Instance
---------------------------------------------------

#. Log in to the console.

#. Click |image1| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click the desired Kafka instance to view its details.

#. .. _kafka-dnat__li122701357121013:

   In the **Connection** area on the **Basic Information** tab page, view and record the private network access addresses of the Kafka instance. In the **Network** area, view and record the VPC and subnet where the Kafka instance is located.


   .. figure:: /_static/images/en-us_image_0000001803492553.png
      :alt: **Figure 1** Kafka instance information

      **Figure 1** Kafka instance information

Step 2: Create a Public NAT Gateway
-----------------------------------

#. Click **Service List** and choose **Network** > **NAT Gateway**.

#. Click **Create Public NAT Gateway**.

#. Set the following parameters:

   -  **Region**: Select the region that the Kafka instance is in.
   -  **Name**: Enter a name for the public NAT gateway.
   -  **VPC**: Select the VPC recorded in :ref:`5 <kafka-dnat__li122701357121013>`.
   -  **Subnet**: Select the subnet recorded in :ref:`5 <kafka-dnat__li122701357121013>`.

   Set other parameters as required. For details, see `Creating a NAT Gateway <https://docs.otc.t-systems.com/usermanual/nat/en-us_topic_0150270259.html>`__.


   .. figure:: /_static/images/en-us_image_0000001614245881.png
      :alt: **Figure 2** Create Public NAT Gateway

      **Figure 2** Create Public NAT Gateway

#. Click **Create Now**.

#. Confirm the specifications and click **Submit**.

Step 3: Add a DNAT Rule
-----------------------

#. On **Public NAT Gateways** page, locate the row containing the newly created public NAT gateway and click **Add Rule** in the **Operation** column.

#. .. _kafka-dnat__li2872030202015:

   On the **DNAT Rules** tab page, click **Add DNAT Rule**.


   .. figure:: /_static/images/en-us_image_0000001614425289.png
      :alt: **Figure 3** Public NAT gateway details

      **Figure 3** Public NAT gateway details

#. Set the following parameters:

   -  **Scenario**: Select **VPC**.
   -  **Port Type**: Select **Specific port**.
   -  **Protocol**: Select **TCP**.
   -  **EIP**: Select an EIP.
   -  **Outside Port**: Enter **9011**.
   -  **Instance Type**: Select **Custom**.
   -  **Private IP Address**: Enter one of the private network addresses of the Kafka instance recorded in :ref:`5 <kafka-dnat__li122701357121013>`.
   -  **Inside Port**: Enter **9011**.

   For details about more parameters, see `Adding a DNAT Rule <https://docs.otc.t-systems.com/usermanual/nat/en-us_topic_0127489530.html>`__.


   .. figure:: /_static/images/en-us_image_0000001563854478.png
      :alt: **Figure 4** Adding a DNAT rule

      **Figure 4** Adding a DNAT rule

#. .. _kafka-dnat__li295532675915:

   Click **OK**.

   View the DNAT rule status in the DNAT rule list. If **Status** is **Running**, the rule has been added successfully.

#. Create DNAT rules for other private network addresses of the Kafka instance recorded in :ref:`5 <kafka-dnat__li122701357121013>`. **Configure a unique EIP for each DNAT rule.**

   For details about how to create a DNAT rule, see :ref:`2 <kafka-dnat__li2872030202015>` to :ref:`4 <kafka-dnat__li295532675915>`.

#. .. _kafka-dnat__li1062193864112:

   After all DNAT rules are created, click the **DNAT Rules** tab to view the created DNAT rules and record the EIPs corresponding to the private IP addresses.

Step 4: Map EIPs to the Port 9011 of Private IP Addresses
---------------------------------------------------------

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click the desired Kafka instance to view its details.

#. In the **Advanced Settings** section on the **Basic Information** tab page, click **Modify** next to **Cross-VPC Access**.

#. Change the values of **advertised.listeners IP Address/Domain Name** to the EIPs in the DNAT rules. Ensure that the mapping between the private network addresses and the EIPs is consistent with that recorded in :ref:`6 <kafka-dnat__li1062193864112>`. Then click **Save**.

   .. _kafka-dnat__fig15689320154314:

   .. figure:: /_static/images/en-us_image_0000001329138322.png
      :alt: **Figure 5** Changing the advertised.listeners IP address (for DNAT access)

      **Figure 5** Changing the advertised.listeners IP address (for DNAT access)

Step 5: Verify Connectivity
---------------------------

Check whether messages can be created and retrieved by referring to :ref:`Connecting to Kafka Using the Client (Plaintext Access) <kafka-ug-180604020>` or :ref:`Connecting to Kafka Using the Client (Ciphertext Access) <kafka-ug-180801001>`.

Notes:

-  The address for connecting to a Kafka instance is in the format of "*advertised.listeners IP*\ **:9011**". For example, the addresses for connecting to the Kafka instance shown in :ref:`Figure 5 <kafka-dnat__fig15689320154314>` are **100.xxx.xxx.20:9011,100.xxx.xxx.21:9011,100.xxx.xxx.23:9011**.
-  Configure security group rules for the Kafka instance to allow inbound access over port **9011**.
-  Public access must be enabled on the client connected to the Kafka instance.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
