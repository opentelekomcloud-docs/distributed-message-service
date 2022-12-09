:original_name: kafka-faq-0003.html

.. _kafka-faq-0003:

What Should I Do If Kafka Storage Space Is Used Up Because Retrieved Messages Are Not Deleted?
==============================================================================================

Messages are not deleted immediately after being retrieved. They are deleted only when the aging time expires.

You can :ref:`shorten the aging time <kafka-ug-200506001>`.
