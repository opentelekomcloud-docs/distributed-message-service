:original_name: Kafka-config.html

.. _Kafka-config:

Collecting Connection Information
=================================

Before accessing a Kafka instance for message production and consumption, obtain the following information of the instance.

Instance Connection Address and Port
------------------------------------

Obtain them from the **Basic Information** page on the Kafka console.

For a cluster Kafka instance that has at least three connection addresses, you are advised to configure all of the connection addresses on the client for high reliability.

For public network access, you can use the public network addresses displayed on the **Basic Information** page.


.. figure:: /_static/images/en-us_image_0000001949896476.png
   :alt: **Figure 1** Viewing the connection addresses and ports of brokers of a Kafka instance

   **Figure 1** Viewing the connection addresses and ports of brokers of a Kafka instance

Topic name
----------

Obtain the topic name from the **Topics** page of the Kafka instance console.

.. note::

   If **Automatic Topic Creation** is disabled, a topic must be created first. Then a Kafka instance can be accessed from a client for message production and consumption.

Ciphertext Access
-----------------

If ciphertext access is enabled for the instance, obtain the instance username and password, SASL mechanism, and security protocol. In addition, obtain the SSL certificate if the security protocol is set to **SASL_SSL**.

-  Obtain the username on the **Users** page on the Kafka console. If you forget your password, obtain it again by `resetting the password <https://docs.otc.t-systems.com/en-us/usermanual/dms/kafka-ug-0003.html>`__.


   .. figure:: /_static/images/en-us_image_0000001980576777.png
      :alt: **Figure 2** Obtaining the SASL_SSL username

      **Figure 2** Obtaining the SASL_SSL username

-  Obtain the SASL mechanism from the **Basic Information** page on the Kafka console.

   If both SCRAM-SHA-512 and PLAIN are enabled, use either of them in connection configurations. For instances that were created much earlier, if **SASL Mechanism** is not displayed on the instance details page, PLAIN is used by default.


   .. figure:: /_static/images/en-us_image_0000001980456929.png
      :alt: **Figure 3** SASL mechanism in use

      **Figure 3** SASL mechanism in use

-  Obtain the security protocol from the **Basic Information** page on the Kafka console. For Kafka instances that were created much earlier, if **Security Protocol** is not displayed on the instance details page, SASL_SSL is used by default.


   .. figure:: /_static/images/en-us_image_0000001980576785.png
      :alt: **Figure 4** Security protocol

      **Figure 4** Security protocol

-  If **Security Protocol** is set to **SASL_SSL**, download the certificate from the **Basic Information** page on the Kafka console.

   JKS certificates are used for accessing instances in Java. CRT certificates are used for accessing instances in Python.


   .. figure:: /_static/images/en-us_image_0000001950565600.png
      :alt: **Figure 5** Downloading the SSL certificate

      **Figure 5** Downloading the SSL certificate
