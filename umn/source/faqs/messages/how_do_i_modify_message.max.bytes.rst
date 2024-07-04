:original_name: kafka_faq_0058.html

.. _kafka_faq_0058:

How Do I Modify message.max.bytes?
==================================

**message.max.bytes** can be modified on the **Parameters** page on the console. For details, see :ref:`Modifying Kafka Instance Configuration Parameters <kafka-ug-0007>`.

The maximum value of **message.max.bytes** is 10,485,760 bytes. If a single message is larger than this size, compress the message with algorithms or split it in the service logic.
