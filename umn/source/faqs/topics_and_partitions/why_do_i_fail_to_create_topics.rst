:original_name: kafka-faq-200426026.html

.. _kafka-faq-200426026:

Why Do I Fail to Create Topics?
===============================

Possible cause: The aggregate number of partitions of created topics has reached the upper limit. The maximum number of partitions varies with instance specifications. For details, see :ref:`Specifications <kafka-specification>`.

Solution: :ref:`Delete unnecessary topics <kafka-ug-180604019>`.
