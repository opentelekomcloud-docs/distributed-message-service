:original_name: kafka-faq-0066.html

.. _kafka-faq-0066:

Why Is Production Rate Still 0 When There Are Produced Messages?
================================================================

The metric data of the message production rate is reported once every minute. Message production rate = Number of messages produced per minute/60. The value is rounded down. The production rate is displayed as 0 if the number of messages produced within a minute is less than 60.
