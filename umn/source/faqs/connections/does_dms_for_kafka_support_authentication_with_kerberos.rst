:original_name: kafka-faq-200426023.html

.. _kafka-faq-200426023:

Does DMS for Kafka Support Authentication with Kerberos?
========================================================

No, Kerberos authentication is not supported. Kafka supports client authentication with SASL and API calling authentication using tokens and AK/SK.

To access an instance in SASL mode, you need the certificates provided by DMS. For details, see :ref:`Connecting to Kafka Using the Client (Ciphertext Access) <kafka-ug-180801001>`.
