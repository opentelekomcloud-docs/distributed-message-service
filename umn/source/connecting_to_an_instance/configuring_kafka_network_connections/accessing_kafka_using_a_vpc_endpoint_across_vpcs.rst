:original_name: kafka-ug-0001.html

.. _kafka-ug-0001:

Accessing Kafka Using a VPC Endpoint Across VPCs
================================================

VPCs are logically isolated from each other. If a Kafka instance and a Kafka client are in different VPCs within a region, they cannot communicate with each other. In this case, you can use one of the following methods to access a Kafka instance across VPCs:

-  Establish a VPC peering connection to allow two VPCs to communicate with each other. For details, see `VPC Peering Connection <https://docs.otc.t-systems.com/en-us/usermanual/vpc/vpc_peering_0000.html>`__.
-  Use VPC Endpoint (VPCEP) to establish a cross-VPC connection.

The following describes how to use VPCEP to implement cross-VPC access.

VPCEP provides two types of resources: VPC endpoint services and VPC endpoints.

-  A VPC endpoint service can be a Kafka instance which is accessed using VPC endpoints.
-  A VPC endpoint is a secure and private channel for connecting a VPC to a VPC endpoint service.


.. figure:: /_static/images/en-us_image_0000001376864660.png
   :alt: **Figure 1** Working principle of accessing a Kafka instance across VPCs

   **Figure 1** Working principle of accessing a Kafka instance across VPCs

Is Plaintext Access or Ciphertext Access Used When a Client Accesses Kafka Across VPCs Using A VPC Endpoint?
------------------------------------------------------------------------------------------------------------

It depends on **Cross-VPC Access Protocol**. The cross-VPC access protocol can be configured when you create a Kafka instance. After an instance is created, the setting cannot be changed.

Options:

-  PLAINTEXT: There is no authentication required in such a connection and data is transmitted in plaintext.
-  SASL_SSL: Clients can connect to a Kafka instance with SASL and the data will be encrypted using the SSL certificate.
-  SASL_PLAINTEXT: Clients can connect to a Kafka instance with SASL and the data will be transmitted in plaintext.

Creating a VPC Endpoint Service
-------------------------------

#. Log in to the console.

#. Click |image1| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click the desired Kafka instance to view its details.

#. .. _kafka-ug-0001__li1470016488194:

   In the **Advanced Settings** section on the **Basic Information** tab page, obtain the listeners IP addresses and port IDs of the instance for **Cross-VPC Access**.


   .. figure:: /_static/images/en-us_image_0000002064922489.png
      :alt: **Figure 2** Cross-VPC access-related listeners IP addresses and corresponding port IDs of the Kafka instance

      **Figure 2** Cross-VPC access-related listeners IP addresses and corresponding port IDs of the Kafka instance

#. In the **Network** section on the **Basic Information** tab page, view the VPC to which the Kafka instance belongs.


   .. figure:: /_static/images/en-us_image_0000002064933413.png
      :alt: **Figure 3** Viewing the VPC to which the Kafka instance belongs

      **Figure 3** Viewing the VPC to which the Kafka instance belongs

#. .. _kafka-ug-0001__li19701310122315:

   Click the VPC to obtain the VPC ID on the VPC console.


   .. figure:: /_static/images/en-us_image_0000002065020989.png
      :alt: **Figure 4** Obtaining the VPC ID

      **Figure 4** Obtaining the VPC ID

#. .. _kafka-ug-0001__li11323122315289:

   Call the VPC Endpoint API to create a VPC endpoint service. For details, see `Creating a VPC Endpoint Service <https://docs.otc.t-systems.com/en-us/api/vpcep/vpcep_06_0201.html>`__.

   .. code-block:: text

      POST https://{endpoint}/v1/{project_id}/vpc-endpoint-services

   Set the following request parameter to the specified values, and other parameters as required.

   -  **port_id**: one of the port IDs obtained in :ref:`5 <kafka-ug-0001__li1470016488194>`.
   -  **vpc_id**: VPC ID obtained in :ref:`7 <kafka-ug-0001__li19701310122315>`.
   -  **server_type**: **VM**
   -  **client_port**: **9011**
   -  **server_port**: **9011**
   -  **protocol**: **TCP**
   -  **approval_enabled**: **false**
   -  **service_type**: **interface**
   -  **endpoint**: VPCEP endpoint obtained from `Regions and Endpoints <https://docs.otc.t-systems.com/en-us/endpoint/index.html>`__. The region must be the same as that of the Kafka instance.
   -  **project_id**: project ID obtained from `Obtaining a Project ID <https://docs.otc.t-systems.com/en-us/api/vpcep/vpcep_08_0003.html>`__. The region must be the same as that of the Kafka instance.

   Record the value of **service_name** in the response. This parameter indicates the name of the VPC endpoint service.

#. .. _kafka-ug-0001__li7368125918119:

   Repeat :ref:`8 <kafka-ug-0001__li11323122315289>` to create VPC endpoint services for other port IDs obtained in :ref:`5 <kafka-ug-0001__li1470016488194>` and record the VPC endpoint service names.

(Optional) Adding a Whitelist
-----------------------------

The VPC endpoint service can be used across accounts through a whitelist.

If the Kafka client and Kafka instance belong to different accounts, add the ID of the account to which the Kafka client belongs to the whitelist of the endpoint service. For details, see `Add a Whitelist Record <https://docs.otc.t-systems.com/en-us/usermanual/vpcep/vpcep_02_02034.html>`__.

Creating a VPC Endpoint
-----------------------

#. .. _kafka-ug-0001__li182701720183719:

   Click **Service List**. Then choose **Network** > **VPC Endpoint**.

#. Click **Create VPC Endpoint**.

#. Set the following parameters:

   -  **Region**: Select the region that the Kafka instance is in.
   -  **Service Category**: Select **Find a service by name**.
   -  **VPC Endpoint Service Name**: Enter the VPC endpoint service name recorded in :ref:`8 <kafka-ug-0001__li11323122315289>` and click **Verify**. If **Service name found** is displayed, proceed with subsequent operations.
   -  **VPC**: Select the VPC that the Kafka client is in.
   -  **Subnet**: Select the subnet that the Kafka client is in.
   -  **Private IP Address**: Select **Automatic**.

   Retain the default values for other parameters. For details, see `Creating a VPC Endpoint <https://docs.otc.t-systems.com/usermanual/vpcep/en-us_topic_0131645189.html>`__.

#. Click **Create Now**.

#. Confirm the configurations and submit the request.

#. Go back to the VPC endpoint list and check whether the status of the created VPC endpoint has changed to **Accepted**. The **Accepted** state means that the VPC endpoint has been connected to the VPC endpoint service.


   .. figure:: /_static/images/en-us_image_0000001380194201.png
      :alt: **Figure 5** Checking the VPC endpoint status

      **Figure 5** Checking the VPC endpoint status

#. .. _kafka-ug-0001__li1942253845112:

   Click the VPC endpoint ID. On the **Summary** tab page, obtain the private IP address.

   You can use the private IP address to access the VPC endpoint service.


   .. figure:: /_static/images/en-us_image_0000001328954164.png
      :alt: **Figure 6** Viewing the private IP address

      **Figure 6** Viewing the private IP address

#. .. _kafka-ug-0001__li923645116109:

   Repeat :ref:`1 <kafka-ug-0001__li182701720183719>` to :ref:`7 <kafka-ug-0001__li1942253845112>` to create a VPC endpoint for each VPC endpoint service created in :ref:`9 <kafka-ug-0001__li7368125918119>`, and view and record the private IP addresses of the VPC endpoint services.

Modifying Parameter advertised.listeners IP
-------------------------------------------

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click the desired Kafka instance to view its details.

#. On the **Advanced Settings** section of the **Basic Information** tab page, click **Modify** for **Cross-VPC Access** to change the value of **advertised.listeners IP address** to the private IP addresses recorded in :ref:`7 <kafka-ug-0001__li1942253845112>` and :ref:`8 <kafka-ug-0001__li923645116109>`. Click **Save**.

   .. important::

      Each IP address must match the corresponding port ID. Otherwise, the network will be disconnected.

   .. _kafka-ug-0001__fig6446112151915:

   .. figure:: /_static/images/en-us_image_0000002064945101.png
      :alt: **Figure 7** Changing the advertised.listeners IP addresses

      **Figure 7** Changing the advertised.listeners IP addresses

Verifying Connectivity
----------------------

Check whether messages can be created and retrieved by referring to :ref:`Connecting to Kafka Using the Client (Plaintext Access) <kafka-ug-180604020>` or :ref:`Connecting to Kafka Using the Client (Ciphertext Access) <kafka-ug-180801001>`.

Notes:

-  The address for connecting to a Kafka instance is in the format of "*advertised.listeners IP*\ **:9011**". For example, the addresses for connecting to the Kafka instance shown in :ref:`Figure 7 <kafka-ug-0001__fig6446112151915>` are **10.158.0.151:9011,10.158.0.162:9011,10.158.0.164:9011**.
-  Configure inbound rules for the security group of the Kafka instance to allow access from **198.19.128.0/17** over port **9011**.
-  If a network access control list (ACL) has been configured for the subnet of this instance, configure inbound rules for the network ACL to allow access from **198.19.128.0/17** and from the subnet used by the VPC endpoint.

.. note::

   **198.19.128.0/17** is the network segment allocated to the VPCEP service. To use VPCEP, allow access from this network segment.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
