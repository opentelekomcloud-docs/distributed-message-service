:original_name: kafka_faq_0062.html

.. _kafka_faq_0062:

How Do I Change the Security Protocol?
======================================

There are two security protocols for Kafka instances: SASL_SSL and SASL_PLAINTEXT.

-  For instances with IPv6 disabled, the security protocol can be changed on the console. In the **Connection** area on the Kafka instance details page, disable **Ciphertext Access** and then configure security protocol when you enable **Ciphertext Access** again.
-  For instances with IPv6 enabled, the security protocol cannot be modified after the instances are created.
