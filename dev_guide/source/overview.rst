:original_name: Kafka-summary.html

.. _Kafka-summary:

Overview
========

Kafka instances are compatible with Apache Kafka and can be accessed using `open-source Kafka clients <https://cwiki.apache.org/confluence/display/KAFKA/Clients>`__. In addition, if **Security Protocol** is set to **SASL_SSL**, use the DMS certificate.

This document describes how to collect instance connection information, such as the instance connection address and topic name. It also provides examples of accessing an instance in Java, Python, and Go.

The examples only demonstrate how to invoke Kafka APIs for producing and consuming messages. For more information about the APIs provided by Kafka, visit the `Kafka official website <https://kafka.apache.org/documentation/#api>`__.

Client Network Environment
--------------------------

A client can access a Kafka instance in any of the following modes:

-  If the client runs an Elastic Cloud Server (ECS) and is in the same region and VPC as the Kafka instance, the client can access the instance using a private network IP address.

-  If the client runs an ECS, and is in the same region but not in the same VPC as the Kafka instance, the client can access the instance using one of the following methods:

   -  Establish a VPC peering connection to allow two VPCs to communicate with each other. For details, see `VPC Peering Connection <https://docs.otc.t-systems.com/en-us/usermanual/vpc/vpc_peering_0000.html>`__. Modify the security group of your Kafka instance as required: Allow external access over port 9092 (in plaintext) or 9093 (in ciphertext).
   -  Access a Kafka instance on a Kafka client over a private network across VPCs using a VPC endpoint. For details, see `Accessing Kafka Across VPCs Using VPCEP <https://docs.otc.t-systems.com/en-us/usermanual/dms/kafka-ug-0001.html>`__. Modify the security group to allow port 9011 for external access.

-  If the client is not in the same network environment or region as the Kafka instance, the client can access the instance using a public network IP address.

   To use public access, modify the security group of your Kafka instance as required: Allow external access over port 9094 (in plaintext) or 9095 (in ciphertext).

.. note::

   The three modes differ only in the connection address for the client to access the instance. This document takes intra-VPC access as an example to describe how to set up the development environment.

   If the connection times out or fails, check the network connectivity. You can use telnet to test the connection address and port of the instance.
