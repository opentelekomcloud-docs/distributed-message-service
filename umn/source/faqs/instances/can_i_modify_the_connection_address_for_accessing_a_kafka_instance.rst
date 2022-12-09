:original_name: kafka-faq-200426011.html

.. _kafka-faq-200426011:

Can I Modify the Connection Address for Accessing a Kafka Instance?
===================================================================

No. You must access a Kafka instance through one of the following ports:

-  Accessing a Kafka instance **without** SASL:

   The port varies with the access mode:

   -  Intra-VPC access: port **9092**
   -  Public access: port **9094**
   -  Cross-VPC access and DNAT access: port **9011**

-  Accessing a Kafka instance **with** SASL:

   The port varies with the access mode:

   -  Intra-VPC access: port **9093**
   -  Public access: port **9095**
   -  Cross-VPC access and DNAT access: port **9011**

Ensure that correct rules have been configured for the security group of the instance. For details, see :ref:`How Do I Select and Configure a Security Group? <kafka-faq-180604024>`
