:original_name: kafka-faq-0604001.html

.. _kafka-faq-0604001:

Troubleshooting Kafka Connection Exceptions
===========================================

Overview
--------

This section describes how to troubleshoot Kafka connection problems.

Problem Classification
----------------------

If the connection to a Kafka instance is abnormal, perform the following operations to troubleshoot the fault:

-  :ref:`Checking the Network <kafka-faq-0604001__section74671936425>`
-  :ref:`Checking Consumer and Producer Configurations <kafka-faq-0604001__section165211131204818>`
-  :ref:`Common Errors on Java Clients <kafka-faq-0604001__section45927511503>`
-  :ref:`Common Errors on the Go Client <kafka-faq-0604001__section105071026185013>`

.. _kafka-faq-0604001__section74671936425:

Checking the Network
--------------------

Before connecting to a Kafka instance, ensure that the client and the instance are interconnected. If they cannot be connected, check the network connection.

For example, if you have enabled SASL_SSL to access the Kafka instance, run the following command:

**curl -kv {ip}:{port}**

-  If the network is normal, information similar to the following is shown:

   |image1|

-  If the network is abnormal or disconnected, information similar to the following is shown:

   |image2|

**Solution:**

#. Check whether the client and the Kafka instance are in the same VPC. If they are not in the same VPC, refer to :ref:`Do Kafka Instances Support Cross-VPC Access? <kafka-faq-200426019>`
#. Check whether the security group rules are correctly configured. For details, see :ref:`How Do I Select and Configure a Security Group? <kafka-faq-180604024>`

.. _kafka-faq-0604001__section165211131204818:

Checking Consumer and Producer Configurations
---------------------------------------------

View logs to check whether the parameters printed during the initialization of the consumer and producer are the same as those set in the configuration files.

If they are different, check the parameters in the configuration file.

.. _kafka-faq-0604001__section45927511503:

Common Errors on Java Clients
-----------------------------

-  **Domain name verification enabled**

   The following error is displayed:

   |image3|

   **Solution**: Check the **consumer.properties** and **producer.properties** files, in which the **ssl.endpoint.identification.algorithm** parameter must be left empty, indicating that domain name verification is disabled.

   .. code-block::

      ssl.endpoint.identification.algorithm=

-  **SSL certificate failing to be loaded**

   The following error is displayed:

   |image4|

   **Solution:**

   #. Check whether the **client.truststore.jks** file exists in the corresponding address.

   #. Check the permissions on the processes and files.

   #. Check whether the **ssl.truststore.password** parameter in the **consumer.properties** and **producer.properties** files is correctly set.

      **ssl.truststore.password** is the server certificate password, which must be set to **dms@kafka** and cannot be changed.

      .. code-block::

         ssl.truststore.password=dms@kafka

-  **Incorrect topic name**

   The following error is displayed:

   |image5|

   **Solution**: Create another topic or enable the automatic topic creation function.

.. _kafka-faq-0604001__section105071026185013:

Common Errors on the Go Client
------------------------------

The Go client fails to connect to Kafka over SSL and the error "first record does not look like a TLS handshake" is returned.

**Solution:** Enable the TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256 cipher suite (which is disabled by default).

.. |image1| image:: /_static/images/en-us_image_0272312053.png
.. |image2| image:: /_static/images/en-us_image_0252483830.png
.. |image3| image:: /_static/images/en-us_image_0252462263.png
.. |image4| image:: /_static/images/en-us_image_0252462634.png
.. |image5| image:: /_static/images/en-us_image_0252462689.png
