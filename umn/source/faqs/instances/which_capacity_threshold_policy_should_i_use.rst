:original_name: kafka-faq-200426007.html

.. _kafka-faq-200426007:

Which Capacity Threshold Policy Should I Use?
=============================================

The following policies are supported:

-  Stop production

   When the memory usage reaches the disk capacity threshold (95%), new messages will no longer be created, but existing messages can still be retrieved until they are discarded. The default retention time is three days. This policy is suitable for scenarios where no data losses can be tolerated.

-  Automatically delete

   When the memory usage reaches the disk capacity threshold (95%), messages can be created and retrieved, but 10% of the earliest messages will be deleted to ensure sufficient disk space. This policy is suitable for scenarios where no service interruption can be tolerated. Data may be lost.

Select a proper policy based on requirements for data and service reliability. Both policies are only used for handling extreme scenarios. **To avoid extreme scenarios, create sufficient disk space in the first place.**
