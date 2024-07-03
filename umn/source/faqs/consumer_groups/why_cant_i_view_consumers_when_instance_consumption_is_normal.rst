:original_name: kafka_faq_0060.html

.. _kafka_faq_0060:

Why Can't I View Consumers When Instance Consumption Is Normal?
===============================================================

Check whether Flink is used for consumption. Flink uses the assign mode and the client assigns specific partitions to be consumed, so you cannot see any consumer on the Kafka console.
