:original_name: kafka-faq-0069.html

.. _kafka-faq-0069:

Why Are Consumer Groups Missing?
================================

If you cannot find a consumer group from the console, the possible causes are as follows:

-  **auto.create.groups.enable** is set to **true**, the consumer group status is **EMPTY**, and no offset has been submitted. The system automatically deletes the consumer group 10 minutes after it is created.
-  If the consumer group has never committed an offset, it will be deleted after the Kafka instance restarts.
