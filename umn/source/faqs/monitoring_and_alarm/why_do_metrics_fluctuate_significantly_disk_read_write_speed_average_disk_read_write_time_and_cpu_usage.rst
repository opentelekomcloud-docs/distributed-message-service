:original_name: kafka-faq-0063.html

.. _kafka-faq-0063:

Why Do Metrics Fluctuate Significantly (Disk Read/Write Speed, Average Disk Read/Write Time, and CPU Usage)?
============================================================================================================

Metrics including **Disk Read Speed**, **Disk Write Speed**, **Average Disk Read Time**, **Average Disk Write Time**, and **CPU Usage** output instantaneous values. These metrics are for reference only. Generally, flushing Kafka data asynchronously to disk consumes disk I/O and CPU usage, causing fluctuations. They do not affect services.
