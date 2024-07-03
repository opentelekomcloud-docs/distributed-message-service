:original_name: kafka-pd-0052.html

.. _kafka-pd-0052:

Comparing Single-node and Cluster Kafka Instances
=================================================

A single-node Kafka instance has only one broker. These instances do not guarantee performance or reliability and are for trial use or testing only. In the production environment, use cluster instances.

Parameters for Creation
-----------------------

Parameter settings that are unique to single-node instances are listed in :ref:`Table 1 <kafka-pd-0052__table156184131315>`.

.. _kafka-pd-0052__table156184131315:

.. table:: **Table 1** Parameters of a single-node instance

   +--------------------------+-------------------------------------------------------------------+
   | Parameter                | Description                                                       |
   +==========================+===================================================================+
   | AZ                       | Only one AZ                                                       |
   +--------------------------+-------------------------------------------------------------------+
   | Version                  | Only v2.7                                                         |
   +--------------------------+-------------------------------------------------------------------+
   | Broker Flavor            | kafka.2u4g.single.small and kafka.2u4g.single                     |
   +--------------------------+-------------------------------------------------------------------+
   | Brokers                  | Only one                                                          |
   +--------------------------+-------------------------------------------------------------------+
   | Storage space per broker | Disk types: high I/O and ultra-high I/O; Disk size: 100-10,000 GB |
   +--------------------------+-------------------------------------------------------------------+
   | Ciphertext Access        | Not supported                                                     |
   +--------------------------+-------------------------------------------------------------------+

Comparing Instance Functions
----------------------------

:ref:`Table 2 <kafka-pd-0052__table16620327103011>` compares the functions of single-node and cluster instances.

.. _kafka-pd-0052__table16620327103011:

.. table:: **Table 2** Comparing functions

   +------------------------------------+-------------------------------------------------+------------------------------------------------+
   | Function                           | Single-node Instance                            | Cluster Instance                               |
   +====================================+=================================================+================================================+
   | Modifying instance specifications  | x                                               | Y                                              |
   +------------------------------------+-------------------------------------------------+------------------------------------------------+
   | Changing the instance access mode  | Only enabling/disabling public plaintext access | Options:                                       |
   |                                    |                                                 |                                                |
   |                                    |                                                 | -  Enabling private ciphertext access          |
   |                                    |                                                 | -  Enabling/Disabling private plaintext access |
   |                                    |                                                 | -  Enabling/Disabling public plaintext access  |
   |                                    |                                                 | -  Enabling/Disabling public ciphertext access |
   +------------------------------------+-------------------------------------------------+------------------------------------------------+
   | Resetting Kafka password           | x                                               | Y                                              |
   +------------------------------------+-------------------------------------------------+------------------------------------------------+
   | Viewing disk usage                 | x                                               | Y                                              |
   +------------------------------------+-------------------------------------------------+------------------------------------------------+
   | Reassigning partitions             | x                                               | Y                                              |
   +------------------------------------+-------------------------------------------------+------------------------------------------------+
   | Configuring topic permissions      | x                                               | Y                                              |
   +------------------------------------+-------------------------------------------------+------------------------------------------------+
   | Managing users                     | x                                               | Y                                              |
   +------------------------------------+-------------------------------------------------+------------------------------------------------+
   | Modifying configuration parameters | x                                               | Y                                              |
   +------------------------------------+-------------------------------------------------+------------------------------------------------+
