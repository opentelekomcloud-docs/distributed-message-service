:original_name: kafka-faq-200426024.html

.. _kafka-faq-200426024:

Is There a Limit on the Number of Topics in a Kafka Instance?
=============================================================

The number of topics is related to the total number of topic partitions and the number of partitions in each topic. There is an upper limit on the aggregate number of partitions of topics. When this limit is reached, no more topics can be created.

The partition limit varies depending on the flavor, as shown in the following table.

.. table:: **Table 1** Kafka instance specifications (cluster)

   +--------------------------+---------+------------------------+-------------------------------+----------------------------------------+---------------------------------------+---------------------+---------------------------+
   | Flavor                   | Brokers | Maximum TPS per Broker | Maximum Partitions per Broker | Recommended Consumer Groups per Broker | Maximum Client Connections per Broker | Storage Space       | Traffic per Broker (MB/s) |
   +==========================+=========+========================+===============================+========================================+=======================================+=====================+===========================+
   | kafka.2u4g.cluster.small | 3-30    | 20,000                 | 100                           | 15                                     | 2000                                  | 300 GB-300,000 GB   | 40                        |
   +--------------------------+---------+------------------------+-------------------------------+----------------------------------------+---------------------------------------+---------------------+---------------------------+
   | kafka.2u4g.cluster       | 3-30    | 30,000                 | 250                           | 20                                     | 2000                                  | 300 GB-300,000 GB   | 100                       |
   +--------------------------+---------+------------------------+-------------------------------+----------------------------------------+---------------------------------------+---------------------+---------------------------+
   | kafka.4u8g.cluster       | 3-30    | 100,000                | 500                           | 100                                    | 4000                                  | 300 GB-600,000 GB   | 200                       |
   +--------------------------+---------+------------------------+-------------------------------+----------------------------------------+---------------------------------------+---------------------+---------------------------+
   | kafka.8u16g.cluster      | 3-50    | 150,000                | 1000                          | 150                                    | 4000                                  | 300 GB-1,500,000 GB | 375                       |
   +--------------------------+---------+------------------------+-------------------------------+----------------------------------------+---------------------------------------+---------------------+---------------------------+
   | kafka.12u24g.cluster     | 3-50    | 200,000                | 1500                          | 200                                    | 4000                                  | 300 GB-1,500,000 GB | 625                       |
   +--------------------------+---------+------------------------+-------------------------------+----------------------------------------+---------------------------------------+---------------------+---------------------------+
   | kafka.16u32g.cluster     | 3-50    | 250,000                | 2000                          | 200                                    | 4000                                  | 300 GB-1,500,000 GB | 750                       |
   +--------------------------+---------+------------------------+-------------------------------+----------------------------------------+---------------------------------------+---------------------+---------------------------+

.. table:: **Table 2** Kafka instance specifications (single-node)

   +-------------------------+---------+----------------+-------------------------------+----------------------------------------+---------------------------------------+------------------+---------------------------+
   | Flavor                  | Brokers | TPS per Broker | Maximum Partitions per Broker | Recommended Consumer Groups per Broker | Maximum Client Connections per Broker | Storage Space    | Traffic per Broker (MB/s) |
   +=========================+=========+================+===============================+========================================+=======================================+==================+===========================+
   | kafka.2u4g.single.small | 1       | 20,000         | 100                           | 15                                     | 2000                                  | 100 GB-10,000 GB | 40                        |
   +-------------------------+---------+----------------+-------------------------------+----------------------------------------+---------------------------------------+------------------+---------------------------+
   | kafka.2u4g.single       | 1       | 30,000         | 250                           | 20                                     | 2000                                  | 100 GB-10,000 GB | 100                       |
   +-------------------------+---------+----------------+-------------------------------+----------------------------------------+---------------------------------------+------------------+---------------------------+
