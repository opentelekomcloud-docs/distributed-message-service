:original_name: kafka-faq-0043.html

.. _kafka-faq-0043:

Will a Consumer Group Without Active Consumers Be Automatically Deleted in 14 Days?
===================================================================================

This depends on the **offsets.retention.minutes** and **auto.create.groups.enable** parameters.

-  For instances created much earlier, **auto.create.groups.enable** is set to **true** by default. **offsets.retention.minutes** determines how long before a consumer group is deleted automatically, which can be changed on the console. For details, see :ref:`Modifying Kafka Instance Configuration Parameters <kafka-ug-0007>`.
-  For newly created instances:

   -  If **auto.create.groups.enable** is **false**, you need to manually delete consumer groups.
   -  If **auto.create.groups.enable** is **true**, a consumer group that has never committed an offset will be automatically deleted after 10 minutes.
   -  If **auto.create.groups.enable** is **true**, and a consumer group has committed an offset, **offsets.retention.minutes** determines how long before the group is deleted automatically, which can be changed on the console. For details, see :ref:`Modifying Kafka Instance Configuration Parameters <kafka-ug-0007>`.

Kafka uses the **offsets.retention.minutes** parameter to control how long to keep offsets for a consumer group. If offsets are not committed within this period, they will be deleted. If Kafka determines that there are no active consumers in a consumer group (for example, when the consumer group is empty) and there are no offsets, Kafka will delete the consumer group.
