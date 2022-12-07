:original_name: kafka-faq-200426009.html

.. _kafka-faq-200426009:

What Is the ZooKeeper Address of a Kafka Instance?
==================================================

Kafka instances are managed using ZooKeeper. Opening ZooKeeper may cause misoperations and service losses. ZooKeeper is used only within Kafka clusters and does not provide services externally.

You can use open-source Kafka clients to connect to Kafka instances and call the native APIs to create and retrieve messages.
