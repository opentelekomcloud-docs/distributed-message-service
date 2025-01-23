:original_name: kafka_ug_0044.html

.. _kafka_ug_0044:

Configuring Plaintext or Ciphertext Access to Kafka Instances
=============================================================

You can access a Kafka instance in plaintext or ciphertext. This section describes how to change the access mode on the console.

-  Plaintext access: Clients connect to the Kafka instance without SASL authentication.
-  Ciphertext access: Clients connect to the Kafka instance with SASL authentication.

.. note::

   -  When you change the access mode for the first time, some instances will restart. You can see the actual situation on the console. The restart takes about 75-80s. The instance will not be restarted when the access mode is changed again.
   -  For a single-node instance, you can only enable or disable plaintext for public network access.
   -  The access mode cannot be changed for instances with IPv6 enabled.

Prerequisites
-------------

You can change the access mode of a Kafka instance only when the instance is in the **Running** state.

Enabling Plaintext Access
-------------------------

#. Log in to the console.

#. Click |image1| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click a Kafka instance to go to the **Basic Information** page.

#. An instance can be accessed in plaintext over the private network and public network. For details about how to enable plaintext access, see :ref:`Table 1 <kafka_ug_0044__table11722031164315>`.

   .. _kafka_ug_0044__table11722031164315:

   .. table:: **Table 1** Enabling plaintext access

      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Access Method                     | Enabling Plaintext Access                                                                                                                                 |
      +===================================+===========================================================================================================================================================+
      | Private network plaintext access  | a. Click |image2| next to **Plaintext Access** in the **Private Network Access** area. A confirmation dialog box is displayed.                            |
      |                                   | b. Click **OK**. The **Background Tasks** page is displayed. If the status of the task turns to **Successful**, plaintext access is successfully enabled. |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Public network plaintext access   | a. Check that **Public Access** is enabled. If it is not enabled, enable it. For details, see :ref:`Configuring Kafka Public Access <kafka-ug-0319001>`.  |
      |                                   | b. Click |image3| next to **Plaintext Access** in the **Public Network Access** area. A confirmation dialog box is displayed.                             |
      |                                   | c. Click **OK**. The **Background Tasks** page is displayed. If the status of the task turns to **Successful**, plaintext access is successfully enabled. |
      +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+

Enabling Ciphertext Access
--------------------------

#. Log in to the console.

#. Click |image4| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click a Kafka instance to go to the **Basic Information** page.

#. An instance can be accessed in ciphertext over the private network and public network. For details about how to enable ciphertext access, see :ref:`Table 2 <kafka_ug_0044__table11522204714587>`.

   .. _kafka_ug_0044__table11522204714587:

   .. table:: **Table 2** Enabling ciphertext access

      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Access Method                     | Enabling Ciphertext Access                                                                                                                                                                                                                                                                                    |
      +===================================+===============================================================================================================================================================================================================================================================================================================+
      | Private network ciphertext access | a. Click |image5| next to **Ciphertext Access** in the **Private Network Access** area. The **Private Network Ciphertext Access** dialog box is displayed.                                                                                                                                                    |
      |                                   | b. Set the :ref:`Kafka security protocol, SASL/PLAIN mechanism, username, and password <kafka_ug_0044__table103011426102317>`, and click **OK**. The **Background Tasks** page is displayed. If the status of the task turns to **Successful**, ciphertext access is successfully enabled.                    |
      |                                   |                                                                                                                                                                                                                                                                                                               |
      |                                   |    .. note::                                                                                                                                                                                                                                                                                                  |
      |                                   |                                                                                                                                                                                                                                                                                                               |
      |                                   |       -  When enabling ciphertext access for the first time (including through private network and public network), you need to set the Kafka security protocol, SASL/PLAIN mechanism, username, and password. Next time when you enable ciphertext access, you only need to set the Kafka security protocol. |
      |                                   |       -  To disable private network ciphertext access, contact customer service.                                                                                                                                                                                                                              |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Public network ciphertext access  | a. Check that **Public Access** is enabled. If it is not enabled, enable it. For details, see :ref:`Configuring Kafka Public Access <kafka-ug-0319001>`.                                                                                                                                                      |
      |                                   | b. Click |image6| next to **Ciphertext Access** in the **Public Network Access** area. The **Public Network Ciphertext Access** dialog box is displayed.                                                                                                                                                      |
      |                                   | c. Set the :ref:`Kafka security protocol, SASL/PLAIN mechanism, username, and password <kafka_ug_0044__table103011426102317>`, and click **OK**. The **Background Tasks** page is displayed. If the status of the task turns to **Successful**, ciphertext access is successfully enabled.                    |
      |                                   |                                                                                                                                                                                                                                                                                                               |
      |                                   |    .. note::                                                                                                                                                                                                                                                                                                  |
      |                                   |                                                                                                                                                                                                                                                                                                               |
      |                                   |       When enabling ciphertext access for the first time (including through private network and public network), you need to set the Kafka security protocol, SASL/PLAIN mechanism, username, and password. Next time when you enable ciphertext access, you only need to set the Kafka security protocol.    |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   The Kafka security protocol, SASL/PLAIN mechanism, username, and password are described as follows.

   .. _kafka_ug_0044__table103011426102317:

   .. table:: **Table 3** Ciphertext access parameters

      +---------------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                 | Value                 | Description                                                                                                                                                                                                              |
      +===========================+=======================+==========================================================================================================================================================================================================================+
      | Security Protocol         | SASL_SSL              | SASL is used for authentication. Data is encrypted with SSL certificates for high-security transmission.                                                                                                                 |
      +---------------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      |                           | SASL_PLAINTEXT        | SASL is used for authentication. Data is transmitted in plaintext for high performance.                                                                                                                                  |
      |                           |                       |                                                                                                                                                                                                                          |
      |                           |                       | SCRAM-SHA-512 authentication is recommended for plaintext transmission.                                                                                                                                                  |
      +---------------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Cross-VPC Access Protocol | ``-``                 | -  When **Plaintext Access** is enabled and **Ciphertext Access** is disabled, **PLAINTEXT** is used for **Cross-VPC Access Protocol**.                                                                                  |
      |                           |                       | -  When **Ciphertext Access** is enabled and **Security Protocol** is **SASL_SSL**, **SASL_SSL** is used for **Cross-VPC Access Protocol**.                                                                              |
      |                           |                       | -  When **Ciphertext Access** is enabled and **Security Protocol** is **SASL_PLAINTEXT**, **SASL_PLAINTEXT** is used for **Cross-VPC Access Protocol**.                                                                  |
      |                           |                       |                                                                                                                                                                                                                          |
      |                           |                       | Fixed once the instance is created.                                                                                                                                                                                      |
      +---------------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | SASL/PLAIN                | ``-``                 | -  If **SASL/PLAIN** is disabled, the SCRAM-SHA-512 mechanism is used for username and password authentication.                                                                                                          |
      |                           |                       | -  If **SASL/PLAIN** is enabled, both the SCRAM-SHA-512 and PLAIN mechanisms are supported. You can select either of them as required.                                                                                   |
      |                           |                       |                                                                                                                                                                                                                          |
      |                           |                       | The **SASL/PLAIN** setting cannot be changed once ciphertext access is enabled.                                                                                                                                          |
      |                           |                       |                                                                                                                                                                                                                          |
      |                           |                       | **What are SCRAM-SHA-512 and PLAIN mechanisms?**                                                                                                                                                                         |
      |                           |                       |                                                                                                                                                                                                                          |
      |                           |                       | -  SCRAM-SHA-512: uses the hash algorithm to generate credentials for usernames and passwords to verify identities. SCRAM-SHA-512 is more secure than PLAIN.                                                             |
      |                           |                       | -  PLAIN: a simple username and password verification mechanism.                                                                                                                                                         |
      +---------------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Username and Password     | ``-``                 | Username and password used by the client to connect to the Kafka instance.                                                                                                                                               |
      |                           |                       |                                                                                                                                                                                                                          |
      |                           |                       | A username should contain 4 to 64 characters, start with a letter, and contain only letters, digits, hyphens (-), and underscores (_).                                                                                   |
      |                           |                       |                                                                                                                                                                                                                          |
      |                           |                       | A password must meet the following requirements:                                                                                                                                                                         |
      |                           |                       |                                                                                                                                                                                                                          |
      |                           |                       | -  Contains 8 to 32 characters.                                                                                                                                                                                          |
      |                           |                       | -  Cannot start with a hyphen (-) and must contain at least three of the following character types: uppercase letters, lowercase letters, digits, spaces, and special characters \`~! @#$\ ``%^&*()-_=+\|[{}];:'",<.>?`` |
      |                           |                       | -  Cannot be the username spelled forward or backward.                                                                                                                                                                   |
      |                           |                       |                                                                                                                                                                                                                          |
      |                           |                       | The username cannot be changed once ciphertext access is enabled.                                                                                                                                                        |
      +---------------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   .. note::

      The Kafka security protocol, SASL/PLAIN mechanism, username, and password are required when the client accesses a Kafka instance with ciphertext access enabled. For details, see :ref:`Connecting to Kafka Using the Client (Ciphertext Access) <kafka-ug-180801001>`.

Disabling Plaintext Access
--------------------------

#. Log in to the console.

#. Click |image7| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click a Kafka instance to go to the **Basic Information** page.

#. An instance can be accessed in plaintext over the private network and public network. For details about how to disable plaintext access, see :ref:`Table 4 <kafka_ug_0044__table442114711262>`.

   .. _kafka_ug_0044__table442114711262:

   .. table:: **Table 4** Disabling plaintext access

      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Access Method                     | Disabling Plaintext Access                                                                                                                                                      |
      +===================================+=================================================================================================================================================================================+
      | Private network plaintext access  | Once enabled, private network access cannot be disabled. Enable plaintext or ciphertext access, or both. If ciphertext access is disabled, plaintext access cannot be disabled. |
      |                                   |                                                                                                                                                                                 |
      |                                   | a. Click |image8| next to **Plaintext Access** in the **Private Network Access** area.                                                                                          |
      |                                   | b. Click **OK**. The **Background Tasks** page is displayed. If the status of the task turns to **Successful**, plaintext access is successfully disabled.                      |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Public network plaintext access   | a. Click |image9| next to **Plaintext Access** in the **Public Network Access** area.                                                                                           |
      |                                   | b. Click **OK**. The **Background Tasks** page is displayed. If the status of the task turns to **Successful**, plaintext access is successfully disabled.                      |
      +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Disabling Ciphertext Access
---------------------------

#. Log in to the console.

#. Click |image10| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click a Kafka instance to go to the **Basic Information** page.

#. An instance can be accessed in ciphertext over the private network and public network. For details about how to disable ciphertext access, see :ref:`Table 5 <kafka_ug_0044__table71031938122916>`.

   .. _kafka_ug_0044__table71031938122916:

   .. table:: **Table 5** Disabling ciphertext access

      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Access Method                     | Disabling Plaintext Access                                                                                                                                  |
      +===================================+=============================================================================================================================================================+
      | Private network ciphertext access | To disable private network ciphertext access, contact customer service.                                                                                     |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Public network ciphertext access  | a. Click |image11| next to **Ciphertext Access** in the **Public Network Access** area.                                                                     |
      |                                   | b. Click **OK**. The **Background Tasks** page is displayed. If the status of the task turns to **Successful**, ciphertext access is successfully disabled. |
      +-----------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------+

   .. note::

      After you disable ciphertext access, the created users will not be deleted. You do not need to create users again when you enable ciphertext access next time.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
.. |image2| image:: /_static/images/en-us_image_0000001191767177.png
.. |image3| image:: /_static/images/en-us_image_0000001191767177.png
.. |image4| image:: /_static/images/en-us_image_0143929918.png
.. |image5| image:: /_static/images/en-us_image_0000001191767177.png
.. |image6| image:: /_static/images/en-us_image_0000001191767177.png
.. |image7| image:: /_static/images/en-us_image_0143929918.png
.. |image8| image:: /_static/images/en-us_image_0000001283221910.png
.. |image9| image:: /_static/images/en-us_image_0000001283221910.png
.. |image10| image:: /_static/images/en-us_image_0143929918.png
.. |image11| image:: /_static/images/en-us_image_0000001283221910.png
