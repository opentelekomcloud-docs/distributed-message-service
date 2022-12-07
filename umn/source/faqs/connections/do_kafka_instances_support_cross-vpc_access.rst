:original_name: kafka-faq-200426019.html

.. _kafka-faq-200426019:

Do Kafka Instances Support Cross-VPC Access?
============================================

Yes. You can use one of the following methods to access a Kafka instance across VPCs:

-  Establish a VPC peering connection to allow two VPCs to communicate with each other. For details, see "Operation Guide" > "VPC Peering Connection" in *Virtual Private Cloud User Guide*.
-  Use VPC Endpoint (VPCEP) to establish a cross-VPC connection. For details, see :ref:`Cross-VPC Access to a Kafka Instance <kafka-ug-0001>`.
