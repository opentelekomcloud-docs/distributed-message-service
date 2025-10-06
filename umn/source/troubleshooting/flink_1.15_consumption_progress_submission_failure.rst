:original_name: kafka_trouble_0007.html

.. _kafka_trouble_0007:

Flink 1.15 Consumption Progress Submission Failure
==================================================

Symptom
-------

To consume Kafka messages in Flink 1.15, the consumption progress fails to be submitted, and the error messages "COORDINATOR_NOT_AVAILABLE" are thrown.

Root Cause
----------

`Bug <https://issues.apache.org/jira/browse/KAFKA-10793>`__ on the Kafka client used by Flink 1.15: When the consumption progress fails to be submitted for once, the client sets the coordinator to unavailable and it cannot be automatically restored.

Solution
--------

-  Restart the Flink job.
-  Upgrade Flink to 1.16 or later.
