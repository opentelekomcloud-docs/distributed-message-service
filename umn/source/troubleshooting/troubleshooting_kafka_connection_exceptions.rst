:original_name: kafka-faq-0604001.html

.. _kafka-faq-0604001:

Troubleshooting Kafka Connection Exceptions
===========================================

Overview
--------

This section describes how to troubleshoot Kafka connection problems.

Problem Classification
----------------------

If the connection to a Kafka instance is abnormal, perform the following operations to troubleshoot the problem:

-  :ref:`Checking the Network <kafka-faq-0604001__en-us_topic_0251961792_section74671936425>`
-  :ref:`Checking Consumer and Producer Configurations <kafka-faq-0604001__en-us_topic_0251961792_section165211131204818>`
-  :ref:`Checking for Common Errors on Java Clients <kafka-faq-0604001__en-us_topic_0251961792_section45927511503>`
-  :ref:`Checking for Common Errors on the Go Client <kafka-faq-0604001__en-us_topic_0251961792_section105071026185013>`

.. _kafka-faq-0604001__en-us_topic_0251961792_section74671936425:

Checking the Network
--------------------

Ensure that the client and the Kafka instance can be connected. If they cannot be connected, check the network.

For example, if you have enabled SASL for the Kafka instance, run the following command:

**curl -kv {ip}:{port}**

-  If the network is normal, information similar to the following is displayed:

   |image1|

-  If the network is abnormal or disconnected, information similar to the following is displayed:

   |image2|

**Solution:**

#. Check whether the client and the Kafka instance are in the same VPC. If no, :ref:`establish a VPC peering connection <kafka-faq-200426019>`.
#. Check whether the security group rules are correctly configured. For details, see :ref:`How Do I Select and Configure a Security Group? <kafka-faq-180604024>`

.. _kafka-faq-0604001__en-us_topic_0251961792_section165211131204818:

Checking Consumer and Producer Configurations
---------------------------------------------

View logs to check whether the parameters printed during initialization of the consumer and producer are the same as those set in the configuration files.

If they are different, check the parameters in the configuration files.

.. _kafka-faq-0604001__en-us_topic_0251961792_section45927511503:

Checking for Common Errors on Java Clients
------------------------------------------

-  Error 1: Domain name verification is not disabled.

   The following error information is displayed:

   |image3|

   **Solution**: Leave the **ssl.endpoint.identification.algorithm** parameter in the **consumer.properties** and **producer.properties** files empty to disable domain name verification.

   .. code-block::

      ssl.endpoint.identification.algorithm=

-  Error 2: SSL certificates fail to be loaded.

   The following error information is displayed:

   |image4|

   **Solution:**

   #. Check whether the **client.jks** file exists in the corresponding address.

   #. Check the permissions on the processes and files.

   #. Check whether the **ssl.truststore.password** parameter in the **consumer.properties** and **producer.properties** files is correctly set.

      **ssl.truststore.password** is the server certificate password, which must be set to **dms@kafka** and cannot be changed.

      .. code-block::

         ssl.truststore.password=dms@kafka

-  Error 3: The topic name is incorrect.

   The following error information is displayed:

   |image5|

   **Solution**: Create a new topic or enable the automatic topic creation function.

.. _kafka-faq-0604001__en-us_topic_0251961792_section105071026185013:

Checking for Common Errors on the Go Client
-------------------------------------------

The Go client fails to connect to Kafka over SSL and the error "first record does not look like a TLS handshake" is returned.

**Solution:** Enable the TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256 cipher suite (which is disabled by default).

.. |image1| image:: /_static/images/en-us_image_0000001073725903.png
.. |image2| image:: /_static/images/en-us_image_0000001074272218.png
.. |image3| image:: /_static/images/en-us_image_0000001074591800.png
.. |image4| image:: /_static/images/en-us_image_0000001073623595.png
.. |image5| image:: /_static/images/en-us_image_0000001073954006.png
