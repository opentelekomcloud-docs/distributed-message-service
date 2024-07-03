:original_name: kafka-ug-180604012.html

.. _kafka-ug-180604012:

Kafka Network Connection Conditions
===================================

A client can connect to a Kafka instance in public or private networks. Notes before using a private network:

-  By default, a client and a Kafka instance are interconnected when they are deployed in a VPC.
-  If they are not, you need to interconnect them because of isolation among VPCs.

:ref:`Table 1 <kafka-ug-180604012__table870241333211>` lists how a client can connect to a Kafka instance.

.. _kafka-ug-180604012__table870241333211:

.. table:: **Table 1** Connection modes

   +----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------+
   | Mode           | How To Do                                                                                                                                                         | Reference                                                                                              |
   +================+===================================================================================================================================================================+========================================================================================================+
   | Public access  | Enable public access on the Kafka console and configure elastic IPs (EIPs). The client can connect to the Kafka instance through EIPs.                            | :ref:`Configuring Kafka Public Access <kafka-ug-0319001>`                                              |
   +----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------+
   |                | Configure port mapping using DNAT. The client can connect to the Kafka instance in a public network.                                                              | :ref:`Accessing Kafka in a Public Network Using DNAT <kafka-dnat>`                                     |
   +----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------+
   | Private access | A client and a Kafka instance are interconnected when they are deployed in a VPC.                                                                                 | ``-``                                                                                                  |
   +----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------+
   |                | When a client and a Kafka instance are deployed in different VPCs of the same region, connect the client and the Kafka instance across VPCs using a VPC endpoint. | :ref:`Accessing Kafka Using a VPC Endpoint Across VPCs <kafka-ug-0001>`                                |
   +----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------+
   |                | When a client and a Kafka instance are deployed in different VPCs of the same region, interconnect two VPCs using a VPC peering connection.                       | `VPC Peering Connection <https://docs.otc.t-systems.com/en-us/usermanual/vpc/vpc_peering_0000.html>`__ |
   +----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------+

Before connecting a client to a Kafka instance, allow accesses for the following security groups.

.. note::

   After a security group is created, its default inbound rule allows communication among ECSs within the security group and its default outbound rule allows all outbound traffic. In this case, you can access a Kafka instance within a VPC, and do not need to add rules according to :ref:`Table 2 <kafka-ug-180604012__table161395381402>`.

.. _kafka-ug-180604012__table161395381402:

.. table:: **Table 2** Security group rules

   +-------------+-------------+-------------+-----------------+---------------------------------------------------------------------------------------+
   | Direction   | Protocol    | Port        | Source          | Description                                                                           |
   +=============+=============+=============+=================+=======================================================================================+
   | Inbound     | TCP         | 9094        | 0.0.0.0/0       | Accessing a Kafka instance over a public network (in plaintext)                       |
   +-------------+-------------+-------------+-----------------+---------------------------------------------------------------------------------------+
   | Inbound     | TCP         | 9092        | 0.0.0.0/0       | -  Accessing a Kafka instance over a private network within a VPC (in plaintext)      |
   |             |             |             |                 | -  Accessing a Kafka instance using a peering connection across VPCs (in plaintext)   |
   +-------------+-------------+-------------+-----------------+---------------------------------------------------------------------------------------+
   | Inbound     | TCP         | 9095        | 0.0.0.0/0       | Accessing a Kafka instance over a public network (in ciphertext)                      |
   +-------------+-------------+-------------+-----------------+---------------------------------------------------------------------------------------+
   | Inbound     | TCP         | 9093        | 0.0.0.0/0       | -  Accessing a Kafka instance over a private network within a VPC (in ciphertext)     |
   |             |             |             |                 | -  Accessing a Kafka instance using a peering connection across VPCs (in ciphertext)  |
   +-------------+-------------+-------------+-----------------+---------------------------------------------------------------------------------------+
   | Inbound     | TCP         | 9011        | 198.19.128.0/17 | Accessing a Kafka instance using a VPC endpoint across VPCs (in cipher- or plaintext) |
   +-------------+-------------+-------------+-----------------+---------------------------------------------------------------------------------------+
   | Inbound     | TCP         | 9011        | 0.0.0.0/0       | Accessing a Kafka instance using DNAT (in cipher- or plaintext)                       |
   +-------------+-------------+-------------+-----------------+---------------------------------------------------------------------------------------+
