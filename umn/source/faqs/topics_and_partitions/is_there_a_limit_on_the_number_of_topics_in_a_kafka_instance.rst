:original_name: kafka-faq-200426024.html

.. _kafka-faq-200426024:

Is There a Limit on the Number of Topics in a Kafka Instance?
=============================================================

The number of topics is related to the total number of topic partitions and the number of partitions in each topic. There is an upper limit on the aggregate number of partitions of topics. When this limit is reached, no more topics can be created.

The partition limit varies depending on the flavor, as shown in the following table.

.. table:: **Table 1** TPS and the maximum number of partitions supported by different instance specifications and I/O types

   +-----------+----------------+-----------------------+-------------------------------+--------------------+
   | Bandwidth | I/O Type       | TPS (High-Throughput) | TPS (Synchronous Replication) | Maximum Partitions |
   +===========+================+=======================+===============================+====================+
   | 100 MB/s  | High I/O       | 100,000               | 60,000                        | 300                |
   +-----------+----------------+-----------------------+-------------------------------+--------------------+
   |           | Ultra-high I/O | 100,000               | 80,000                        | 300                |
   +-----------+----------------+-----------------------+-------------------------------+--------------------+
   | 300 MB/s  | High I/O       | 300,000               | 150,000                       | 900                |
   +-----------+----------------+-----------------------+-------------------------------+--------------------+
   |           | Ultra-high I/O | 300,000               | 200,000                       | 900                |
   +-----------+----------------+-----------------------+-------------------------------+--------------------+
   | 600 MB/s  | Ultra-high I/O | 600,000               | 300,000                       | 1800               |
   +-----------+----------------+-----------------------+-------------------------------+--------------------+
   | 1200 MB/s | Ultra-high I/O | 1,200,000             | 400,000                       | 1800               |
   +-----------+----------------+-----------------------+-------------------------------+--------------------+
