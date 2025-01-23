:original_name: kafka_faq_0052.html

.. _kafka_faq_0052:

How Do I Modify the SASL Mechanism?
===================================

There are two SASL authentication mechanisms for Kafka instances: SCRAM-SHA-512 and PLAIN.

-  For instances with IPv6 disabled, the mechanism cannot be modified after ciphertext access is enabled. If you want to change it, create an instance again.
-  For instances with IPv6 enabled, the mechanism cannot be modified after the instances are created. If you want to change it, create an instance again.
