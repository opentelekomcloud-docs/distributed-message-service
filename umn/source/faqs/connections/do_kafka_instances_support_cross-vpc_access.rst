:original_name: kafka-faq-200426019.html

.. _kafka-faq-200426019:

Do Kafka Instances Support Cross-VPC Access?
============================================

Yes. You can use one of the following methods to access a Kafka instance across VPCs:

-  Establish a VPC peering connection to allow two VPCs to communicate with each other. For details, see `VPC Peering Connection <https://docs.otc.t-systems.com/en-us/usermanual/vpc/vpc_peering_0000.html>`__.
-  Use VPC Endpoint (VPCEP) to establish a cross-VPC connection. For details, see :ref:`Accessing Kafka Using a VPC Endpoint Across VPCs <kafka-ug-0001>`.
