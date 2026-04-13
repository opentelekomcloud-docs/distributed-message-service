:original_name: kafka-faq-0065.html

.. _kafka-faq-0065:

Why Are Offsets Not Continuous?
===============================

If you have enabled idempotence or transactions on the producer client, and produced messages, message offsets are not continuous on the consumer client or on the **Message Query** page on the Kafka console. This is because enabling idempotence or transactions generates some metadata control messages during message production. These control messages are produced to topics, and are invisible to consumers.

By default, idempotence is enabled for Kafka 3.0 and later producer clients. To disable it, set the parameter **enable.idempotence** to **false**.
