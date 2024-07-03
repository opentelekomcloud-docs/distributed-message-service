:original_name: kafka_faq_0061.html

.. _kafka_faq_0061:

Why Is It Not Recommended to Use a Sarama Client for Messaging?
===============================================================

Symptom
-------

If a Sarama client is used to send and receive messages, the following issues may occur:

-  Sarama cannot detect partition changes. Adding topic partitions requires client restart to enable consumption.
-  Sarama's default **MaxProcessingTime** is 100 ms. When this limit is reached, consumers can no longer consume messages.
-  If consumer offsets reset from the oldest (earliest) position, all messages starting from the earliest position may be repeatedly consumed after the client restarts.
-  A consumer that subscribes to multiple topics may not be able to consume any message from specific partitions.

Solution
--------

Use `confluent-kafka-go <https://github.com/confluentinc/confluent-kafka-go>`__ as the Kafka client library.

For details, see :ref:`Table 1 <kafka_faq_0061__table183502571446>`.

.. _kafka_faq_0061__table183502571446:

.. table:: **Table 1** Comparing common Go clients

   +-----------------------+--------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------+
   | Client                | Pros                                                                                                   | Cons                                                                                                               |
   +=======================+========================================================================================================+====================================================================================================================+
   | confluent-kafka-go    | -  An official Kafka client by Confluent that supports full Kafka compatibility and all Kafka features | High compiling complexity because Go compilers need extra resources to configure the imported C++ libraries        |
   |                       | -  High stability and performance, and low latency based on librdkafka                                 |                                                                                                                    |
   +-----------------------+--------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------+
   | kafka-go              | -  A simple and lite Kafka client easy for learning and usage                                          | -  Fewer advanced functions and configurations than confluent-kafka-go                                             |
   |                       | -  Reduced application size and complexity with limited library and fewer dependencies                 | -  Applicable only to simple scenarios that require low performance and throughput                                 |
   +-----------------------+--------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------+
   | Sarama                | Better asynchronization and higher concurrency (written in the original Go language)                   | -  Many bugs, limited documentation                                                                                |
   |                       |                                                                                                        | -  Deteriorates application performance when processing a large number of messages due to large memory consumption |
   +-----------------------+--------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------+
