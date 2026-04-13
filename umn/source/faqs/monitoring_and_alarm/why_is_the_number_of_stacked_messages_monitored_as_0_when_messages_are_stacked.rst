:original_name: kafka-faq-0067.html

.. _kafka-faq-0067:

Why Is the Number of Stacked Messages Monitored as 0 when Messages Are Stacked?
===============================================================================

Symptom
-------

On the **Consumer Offset** tab page of the consumer group details page, there are stacked messages in a topic (total stack ≠ 0), whereas the **Consumer Available Messages** on the consumer group monitoring page is 0.

Conclusion
----------

The total stack on the **Consumer Offset** tab page and the **Consumer Available Messages** are not synchronously updated.

The total stack is sampled immediately. The **Consumer Available Messages** is sampled every minute. You see the stack number at your time. When a consumer consumes all the stacked messages within 1 minute, **Consumer Available Messages** displays 0.
