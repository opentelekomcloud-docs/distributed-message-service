:original_name: kafka-faq-0034.html

.. _kafka-faq-0034:

How Many Connections Are Allowed from Each IP Address?
======================================================

Each Kafka broker allows a maximum of 1000 connections from each IP address by default. Excess connections will be rejected. You can change the limit by referring to :ref:`Modifying Kafka Instance Configuration Parameters <kafka-ug-0007>`.
