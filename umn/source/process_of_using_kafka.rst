:original_name: kafka-ug-0069.html

.. _kafka-ug-0069:

Process of Using Kafka
======================

The following figure shows the process of using a Kafka instance to produce and consume messages.


.. figure:: /_static/images/en-us_image_0000001921463342.png
   :alt: **Figure 1** Process of using Kafka

   **Figure 1** Process of using Kafka

#. :ref:`Creating a User and Granting DMS for Kafka Permissions <createuserandgrantpolicy>`

   Create IAM users and grant them only the DMS for Kafka permissions required to perform a given task based on their job responsibilities.

#. :ref:`Creating a Kafka Instance <kafka-ug-180604013>`

   Kafka instances are tenant-exclusive, and physically isolated in deployment.

#. :ref:`Creating a Kafka Topic <kafka-ug-180604018>`

   Create a topic for storing messages so that producers can produce messages and consumers can subscribe to messages.

#. :ref:`Connecting to an Instance <kafka-ug190605003>`

   The client uses commands to connect to Kafka instances in a private or public network, and produces and consumes messages.

#. :ref:`Managing Messages <kafka-ug-0720002>`

   View messages on the console.
