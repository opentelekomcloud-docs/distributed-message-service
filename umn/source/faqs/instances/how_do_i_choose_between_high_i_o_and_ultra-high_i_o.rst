:original_name: kafka-faq-200426006.html

.. _kafka-faq-200426006:

How Do I Choose Between High I/O and Ultra-high I/O?
====================================================

-  High I/O: The average latency is 6 to 10 ms, and the maximum bandwidth is 150 MB/s (read + write).
-  Ultra-high I/O: The average latency is 1 to 3 ms, and the maximum bandwidth is 350 MB/s (read + write).

You are advised to select ultra-high I/O, because ultra-high I/O disks deliver much higher bandwidth than high I/O.
