:original_name: kafka-faq-0033.html

.. _kafka-faq-0033:

Is There a Limit on the Number of Client Connections to a Kafka Instance?
=========================================================================

Yes. The maximum allowed number of client connections varies by instance specifications.

-  If the bandwidth is 100 MB/s, a maximum of 3000 client connections are allowed.
-  If the bandwidth is 300 MB/s, a maximum of 10,000 client connections are allowed.
-  If the bandwidth is 600 MB/s, a maximum of 20,000 client connections are allowed.
-  If the bandwidth is 1200 MB/s, a maximum of 20,000 client connections are allowed.
