:original_name: kafka-python.html

.. _kafka-python:

Python
======

This section describes how to access a Kafka premium instance using a Kafka client in Python on the Linux CentOS, including how to install the client, and produce and consume messages.

Before getting started, ensure that you have collected the information listed in :ref:`Collecting Connection Information <kafka-config>`.

Preparing the Environment
-------------------------

-  Python

   Generally, Python is pre-installed in the system. Enter **python** in a CLI. If the following information is displayed, Python has already been installed.

   .. code-block:: console

      [root@ecs-test python-kafka]# python3
      Python 3.7.1 (default, Jul  5 2020, 14:37:24)
      [GCC 4.8.5 20150623 (Red Hat 4.8.5-39)] on linux
      Type "help", "copyright", "credits" or "license" for more information.
      >>>

   If Python is not installed, run the following command:

   **yum install python**

-  Kafka clients in Python

   Run the following command to install a Python client of the recommended version:

   **pip install kafka-python==2.0.1**

Producing Messages
------------------

.. note::

   Replace the following information in bold with the actual values.

-  With SASL

   .. code-block::

      from kafka import KafkaProducer
      import ssl
      ##Connection information
      conf = {
          'bootstrap_servers': ["ip1:port1","ip2:port2","ip3:port3"],
          'topic_name': 'topic_name',
          'sasl_plain_username': 'username',
          'sasl_plain_password': 'password'
      }

      context = ssl.create_default_context()
      context = ssl.SSLContext(ssl.PROTOCOL_SSLv23)
      context.verify_mode = ssl.CERT_REQUIRED
      ## Certificate file. For details about how to obtain an SSL certificate, see section "Collecting Connection Information."
      context.load_verify_locations("phy_ca.crt")

      print('start producer')
      producer = KafkaProducer(bootstrap_servers=conf['bootstrap_servers'],
                              sasl_mechanism="PLAIN",
                              ssl_context=context,
                              security_protocol='SASL_SSL',
                              sasl_plain_username=conf['sasl_plain_username'],
                              sasl_plain_password=conf['sasl_plain_password'])

      data = bytes("hello kafka!", encoding="utf-8")
      producer.send(conf['topic_name'], data)
      producer.close()
      print('end producer')

-  Without SASL

   .. code-block::

      from kafka import KafkaProducer

      conf = {
          'bootstrap_servers': ["ip1:port1","ip2:port2","ip3:port3"],
          'topic_name': 'topic-name',
      }

      print('start producer')
      producer = KafkaProducer(bootstrap_servers=conf['bootstrap_servers'])

      data = bytes("hello kafka!", encoding="utf-8")
      producer.send(conf['topic_name'], data)
      producer.close()
      print('end producer')

Consuming Messages
------------------

-  With SASL

   .. code-block::

      from kafka import KafkaConsumer
      import ssl
      ##Connection information
      conf = {
          'bootstrap_servers': ["ip1:port1","ip2:port2","ip3:port3"],
          'topic_name': 'topic_name',
          'sasl_plain_username': 'username',
          'sasl_plain_password': 'password',
          'consumer_id': 'consumer_id'
      }

      context = ssl.create_default_context()
      context = ssl.SSLContext(ssl.PROTOCOL_SSLv23)
      context.verify_mode = ssl.CERT_REQUIRED
      ## Certificate file. For details about how to obtain an SSL certificate, see section "Collecting Connection Information."
      context.load_verify_locations("phy_ca.crt")

      print('start consumer')
      consumer = KafkaConsumer(conf['topic_name'],
                              bootstrap_servers=conf['bootstrap_servers'],
                              group_id=conf['consumer_id'],
                              sasl_mechanism="PLAIN",
                              ssl_context=context,
                              security_protocol='SASL_SSL',
                              sasl_plain_username=conf['sasl_plain_username'],
                              sasl_plain_password=conf['sasl_plain_password'])

      for message in consumer:
          print("%s:%d:%d: key=%s value=%s" % (message.topic, message.partition,message.offset, message.key,message.value))

      print('end consumer')

-  Without SASL

   Replace the information in bold with the actual values.

   .. code-block::

      from kafka import KafkaConsumer

      conf = {
          'bootstrap_servers': ["ip1:port1","ip2:port2","ip3:port3"],
          'topic_name': 'topic-name',
          'consumer_id': 'consumer-id'
      }

      print('start consumer')
      consumer = KafkaConsumer(conf['topic_name'],
                              bootstrap_servers=conf['bootstrap_servers'],
                              group_id=conf['consumer_id'])

      for message in consumer:
          print("%s:%d:%d: key=%s value=%s" % (message.topic, message.partition,message.offset, message.key,message.value))

      print('end consumer')
