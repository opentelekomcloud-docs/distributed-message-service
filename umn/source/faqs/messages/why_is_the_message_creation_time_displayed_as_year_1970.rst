:original_name: kafka-faq-0045.html

.. _kafka-faq-0045:

Why Is the Message Creation Time Displayed as Year 1970?
========================================================

The message creation time is specified by **CreateTime** when a producer creates messages. If this parameter is not set during message creation, the message creation time is year 1970 by default.
