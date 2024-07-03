:original_name: kafka-trouble-0002.html

.. _kafka-trouble-0002:

Troubleshooting Topic Deletion Failures
=======================================

Symptom
-------

A deleted topic still exists.

Root Cause
----------

Automatic topic creation has been enabled for the instance, and a consumer is connecting to the topic. If services are not stopped, message creation will continue, and new topics will be automatically created.

Solution
--------

Disable automatic topic creation for the instance and then try again to delete the topic. For details, see :ref:`Configuring Automatic Topic Creation <kafka_ug_0043>`.
