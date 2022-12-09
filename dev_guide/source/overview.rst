:original_name: Kafka-summary.html

.. _Kafka-summary:

Overview
========

Kafka instances are compatible with Apache Kafka and can be accessed using `open-source Kafka clients <https://cwiki.apache.org/confluence/display/KAFKA/Clients>`__. To access an instance in SASL mode, you will also need certificates.

This document describes how to collect instance connection information, such as the instance connection address, certificate required for SASL connection, and information required for public access. It also provides examples of accessing an instance in Java and Python.

The examples only demonstrate how to invoke Kafka APIs for producing and consuming messages. For more information about the APIs provided by Kafka, visit the `Kafka official website <https://kafka.apache.org/documentation/#api>`__.

Client Network Environment
--------------------------

A client can access a Kafka instance in any of the following modes:

#. Within a Virtual Private Network (VPC)

   If the client runs an Elastic Cloud Server (ECS) and is in the same region and VPC as the Kafka instance, the client can access the instance using an IP address within a subnet in the VPC.

#. Using a VPC peering connection

   If the client runs an ECS and is in the same region but not the same VPC as the Kafka instance, the client can access the instance using an IP address within a subnet in the VPC after a VPC peering connection has been established.

#. Over public networks

   If the client is not in the same network environment or region as the Kafka instance, the client can access the instance using a public network IP address.

   For public access, modify the inbound rules of the security group configured for the Kafka instance, allowing access over port 9094 or 9095.

.. note::

   The three modes differ only in the connection address for the client to access the instance. This document takes intra-VPC access as an example to describe how to set up the development environment.

   If the connection times out or fails, check the network connectivity. You can use telnet to test the connection address and port of the instance.
