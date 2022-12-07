:original_name: kafka-faq-0043.html

.. _kafka-faq-0043:

Will a Consumer Group Without Active Consumers Be Automatically Deleted in 14 Days?
===================================================================================

Yes.

Kafka uses the **offsets.retention.minutes** parameter to control how long to keep offsets for a consumer group. If offsets are not committed within this period, they will be deleted. The default value of **offsets.retention.minutes** is 20,160 minutes (14 days).

If Kafka determines that there are no active consumers in a consumer group (for example, when the consumer group is empty) and there are no offsets, Kafka will delete the consumer group.
