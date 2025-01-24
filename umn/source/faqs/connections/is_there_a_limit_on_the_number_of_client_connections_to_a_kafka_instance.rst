:original_name: kafka-faq-0033.html

.. _kafka-faq-0033:

Is There a Limit on the Number of Client Connections to a Kafka Instance?
=========================================================================

Yes. The maximum allowed number of client connections varies by instance specifications.

.. table:: **Table 1** Number of connections of earlier Kafka instances

   ================= ================
   Assured Bandwidth Max. Connections
   ================= ================
   100 MB/s          3000
   300 MB/s          10,000
   600 MB/s          20,000
   1200 MB/s         20,000
   ================= ================

.. table:: **Table 2** Number of connections of later Kafka instances

   ======================== ==================================
   Flavor                   Max. Client Connections per Broker
   ======================== ==================================
   kafka.2u4g.cluster.small 2000
   kafka.2u4g.single.small  2000
   kafka.2u4g.cluster       2000
   kafka.2u4g.single        2000
   kafka.4u8g.cluster       4000
   kafka.8u16g.cluster      4000
   kafka.12u24g.cluster     4000
   kafka.16u32g.cluster     4000
   ======================== ==================================
