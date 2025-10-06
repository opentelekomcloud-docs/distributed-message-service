:original_name: kafka-pd-0052.html

.. _kafka-pd-0052:

Comparing Single-node and Cluster Kafka Instances
=================================================

A single-node Kafka instance has only one broker. These instances do not guarantee performance or reliability and are for trial use or testing only. In the production environment, use cluster instances.

:ref:`Table 1 <kafka-pd-0052__table16620327103011>` compares single-node and cluster instances by features and functions.

.. _kafka-pd-0052__table16620327103011:

.. table:: **Table 1** Comparing single-node and cluster instances

   +------------------------------------+------------------+---------------------------------+
   | Item                               | Single-node      | Cluster                         |
   +====================================+==================+=================================+
   | Version                            | 2.7              | 1.1.0, 2.3.0, 2.7, and 3.x      |
   +------------------------------------+------------------+---------------------------------+
   | AZ                                 | Single           | 1, or 3 or more                 |
   +------------------------------------+------------------+---------------------------------+
   | Brokers                            | 1                | 3 and more                      |
   +------------------------------------+------------------+---------------------------------+
   | Access mode                        | Plaintext access | Plaintext and ciphertext access |
   +------------------------------------+------------------+---------------------------------+
   | Modifying instance specifications  | x                | Y                               |
   +------------------------------------+------------------+---------------------------------+
   | Resetting Kafka password           | x                | Y                               |
   +------------------------------------+------------------+---------------------------------+
   | Viewing disk usage                 | x                | Y                               |
   +------------------------------------+------------------+---------------------------------+
   | Reassigning partitions             | x                | Y                               |
   +------------------------------------+------------------+---------------------------------+
   | Configuring topic permissions      | x                | Y                               |
   +------------------------------------+------------------+---------------------------------+
   | Managing users                     | x                | Y                               |
   +------------------------------------+------------------+---------------------------------+
   | Smart Connect                      | x                | Y                               |
   +------------------------------------+------------------+---------------------------------+
   | Modifying configuration parameters | x                | Y                               |
   +------------------------------------+------------------+---------------------------------+
