:original_name: kafka-faq-180604024.html

.. _kafka-faq-180604024:

How Do I Select and Configure a Security Group?
===============================================

Kafka instances can be accessed within a VPC, across VPCs, through DNAT, or over public networks. Before accessing a Kafka instance, configure a security group.

Intra-VPC Access
----------------

#. Check whether the client and instance use the same security group.

   -  If they use the same security group, check whether the security group has the default inbound rule that allows communication among ECSs within the security group and the default outbound rule that allows all outbound traffic. If these rules are available, you do not need to add more rules. If these rules are not available, add rules according to :ref:`Table 1 <kafka-faq-180604024__table1665584042410>`.

      .. _kafka-faq-180604024__table1665584042410:

      .. table:: **Table 1** Security group rules

         +-----------+----------+------+------+-----------+--------------------------------------------------------------------------------+
         | Direction | Protocol | Type | Port | Source    | Description                                                                    |
         +===========+==========+======+======+===========+================================================================================+
         | Inbound   | TCP      | IPv4 | 9092 | 0.0.0.0/0 | Accessing a Kafka instance over a private network within a VPC (in plaintext)  |
         +-----------+----------+------+------+-----------+--------------------------------------------------------------------------------+
         | Inbound   | TCP      | IPv6 | 9192 | ::/0      | Accessing a Kafka instance within a VPC (with SSL encryption disabled)         |
         +-----------+----------+------+------+-----------+--------------------------------------------------------------------------------+
         | Inbound   | TCP      | IPv4 | 9093 | 0.0.0.0/0 | Accessing a Kafka instance over a private network within a VPC (in ciphertext) |
         +-----------+----------+------+------+-----------+--------------------------------------------------------------------------------+
         | Inbound   | TCP      | IPv6 | 9193 | ::/0      | Accessing a Kafka instance within a VPC (with SSL encryption enabled)          |
         +-----------+----------+------+------+-----------+--------------------------------------------------------------------------------+

   -  If they use different security groups, go to :ref:`2 <kafka-faq-180604024__li128055103219>`.

#. .. _kafka-faq-180604024__li128055103219:

   Configure security group rules as follows.

   Assume that the security groups of the client and Kafka instance are **sg-53d4** and **Default_All**, respectively. You can specify a security group or IP address as the destination in the following rule. A security group is used as an example.

   To ensure that your client can access the Kafka instance, add the following rule to the security group configured for the client:

   .. table:: **Table 2** Security group rule

      ========= ====== =============== ===========
      Direction Action Protocol & Port Destination
      ========= ====== =============== ===========
      Outbound  Allow  All             Default_All
      ========= ====== =============== ===========

   To ensure that your client can access the Kafka instance, add the following rule to the security group configured for the instance.

   .. table:: **Table 3** Security group rule

      ========= ====== =============== =======
      Direction Action Protocol & Port Source
      ========= ====== =============== =======
      Inbound   Allow  All             sg-53d4
      ========= ====== =============== =======

Cross-VPC and DNAT-based Instance Access
----------------------------------------

Configure security group rules according to :ref:`Table 4 <kafka-faq-180604024__table11349192018326>`.

.. _kafka-faq-180604024__table11349192018326:

.. table:: **Table 4** Security group rules

   +-----------+----------+------+-----------------+---------------------------------------------------------------------------------------+
   | Direction | Protocol | Port | Source          | Description                                                                           |
   +===========+==========+======+=================+=======================================================================================+
   | Inbound   | TCP      | 9011 | 198.19.128.0/17 | Accessing a Kafka instance using a VPC endpoint across VPCs (in cipher- or plaintext) |
   +-----------+----------+------+-----------------+---------------------------------------------------------------------------------------+
   | Inbound   | TCP      | 9011 | 0.0.0.0/0       | Accessing a Kafka instance using DNAT (in cipher- or plaintext)                       |
   +-----------+----------+------+-----------------+---------------------------------------------------------------------------------------+
   | Inbound   | TCP      | 9092 | 0.0.0.0/0       | Accessing a Kafka instance using a peering connection across VPCs (in plaintext)      |
   +-----------+----------+------+-----------------+---------------------------------------------------------------------------------------+
   | Inbound   | TCP      | 9093 | 0.0.0.0/0       | Accessing a Kafka instance using a peering connection across VPCs (in ciphertext)     |
   +-----------+----------+------+-----------------+---------------------------------------------------------------------------------------+

Public Access
-------------

Configure security group rules according to :ref:`Table 5 <kafka-faq-180604024__table221215285815>`.

.. _kafka-faq-180604024__table221215285815:

.. table:: **Table 5** Security group rules

   +-----------+----------+------+------+-----------+------------------------------------------------------------------+
   | Direction | Protocol | Type | Port | Source    | Description                                                      |
   +===========+==========+======+======+===========+==================================================================+
   | Inbound   | TCP      | IPv4 | 9094 | 0.0.0.0/0 | Accessing a Kafka instance over a public network (in plaintext)  |
   +-----------+----------+------+------+-----------+------------------------------------------------------------------+
   | Inbound   | TCP      | IPv4 | 9095 | 0.0.0.0/0 | Accessing a Kafka instance over a public network (in ciphertext) |
   +-----------+----------+------+------+-----------+------------------------------------------------------------------+
   | Inbound   | TCP      | IPv6 | 9192 | ::/0      | Accessing a Kafka instance over a public network (without SSL)   |
   +-----------+----------+------+------+-----------+------------------------------------------------------------------+
   | Inbound   | TCP      | IPv6 | 9193 | ::/0      | Accessing a Kafka instance over a public network (with SSL)      |
   +-----------+----------+------+------+-----------+------------------------------------------------------------------+
