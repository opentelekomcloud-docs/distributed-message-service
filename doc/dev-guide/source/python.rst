:original_name: kafka-python.html

.. _kafka-python:

Python
======

This section takes Linux CentOS as an example to describe how to access a Kafka instance using a Kafka client in Python, including how to install the client, and produce and consume messages.

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

-  With SASL

   .. code-block::

      from kafka import KafkaProducer
      import ssl
      ##Connection information
      conf = {
          'bootstrap_servers': ["ip1:port1","ip2:port2","ip3:port3"],
          'topic_name': 'topic_name',
          'sasl_username': 'username',
          'sasl_password': 'password'
      }

      context = ssl.create_default_context()
      context = ssl.SSLContext(ssl.PROTOCOL_SSLv23)
      ## If Security Protocol is set to SASL_PLAINTEXT, comment out the following parameters:
      context.verify_mode = ssl.CERT_REQUIRED
      ## The certificate file. Obtain the SSL certificate by referring to "Collecting Connection Information". If Security Protocol is set to SASL_PLAINTEXT, comment out the following parameters:
      context.load_verify_locations("phy_ca.crt")

      print('start producer')
      producer = KafkaProducer(bootstrap_servers=conf['bootstrap_servers'],
                              sasl_mechanism="PLAIN",
                              ssl_context=context,
                              security_protocol='SASL_SSL',
                              sasl_plain_username=conf['sasl_username'],
                              sasl_plain_password=conf['sasl_password'])

      data = bytes("hello kafka!", encoding="utf-8")
      producer.send(conf['topic_name'], data)
      producer.close()
      print('end producer')

   The parameters in the example code are described as follows. For details about how to obtain the parameter values, see :ref:`Collecting Connection Information <kafka-config>`.

   -  **bootstrap_servers**: instance connection address and port
   -  **topic_name**: topic name
   -  **sasl_plain_username/sasl_plain_password**: The username and password set when ciphertext access is enabled for the first time, or the ones set in user creation. For security purposes, you are advised to encrypt the username and password.
   -  **context.load_verify_locations**: certificate file. This parameter is mandatory when **Security Protocol** is set to **SASL_SSL**. CRT certificates are used for accessing instances in Python.
   -  **sasl_mechanism**: SASL authentication mechanism. View it on the **Basic Information** page of the Kafka instance console. If both SCRAM-SHA-512 and PLAIN are enabled, use either of them in connection configurations. For instances that were created much earlier, if **SASL Mechanism** is not displayed on the instance details page, PLAIN is used by default.
   -  **security_protocol**: Kafka security protocol. Obtain it from the **Basic Information** page on the Kafka console. For Kafka instances that were created much earlier, if **Security Protocol** is not displayed on the instance details page, SASL_SSL is used by default.

      -  When **Security Protocol** is set to **SASL_SSL**, SASL is used for authentication. Data is encrypted with SSL certificates for high-security transmission. You need to configure the instance username, password, and certificate file.
      -  When **Security Protocol** is set to **SASL_PLAINTEXT**, SASL is used for authentication. Data is transmitted in plaintext with high performance. You need to configure the instance username and password.

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

   The parameters in the example code are described as follows. For details about how to obtain the parameter values, see :ref:`Collecting Connection Information <kafka-config>`.

   -  **bootstrap_servers**: instance connection address and port
   -  **topic_name**: topic name

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
          'sasl_username': 'username',
          'sasl_password': 'password',
          'consumer_id': 'consumer_id'
      }

      context = ssl.create_default_context()
      context = ssl.SSLContext(ssl.PROTOCOL_SSLv23)
      ## If Security Protocol is set to SASL_PLAINTEXT, comment out the following parameters:
      context.verify_mode = ssl.CERT_REQUIRED
      ## The certificate file. Obtain the SSL certificate by referring to "Collecting Connection Information". If Security Protocol is set to SASL_PLAINTEXT, comment out the following parameters:
      context.load_verify_locations("phy_ca.crt")

      print('start consumer')
      consumer = KafkaConsumer(conf['topic_name'],
                              bootstrap_servers=conf['bootstrap_servers'],
                              group_id=conf['consumer_id'],
                              sasl_mechanism="PLAIN",
                              ssl_context=context,
                              security_protocol='SASL_SSL',
                              sasl_plain_username=conf['sasl_username'],
                              sasl_plain_password=conf['sasl_password'])

      for message in consumer:
          print("%s:%d:%d: key=%s value=%s" % (message.topic, message.partition,message.offset, message.key,message.value))

      print('end consumer')

   The parameters in the example code are described as follows. For details about how to obtain the parameter values, see :ref:`Collecting Connection Information <kafka-config>`.

   -  **bootstrap_servers**: instance connection address and port
   -  **topic_name**: topic name
   -  **sasl_plain_username/sasl_plain_password**: The username and password set when ciphertext access is enabled for the first time, or the ones set in user creation. For security purposes, you are advised to encrypt the username and password.
   -  **consumer_id**: custom consumer group name. If the specified consumer group does not exist, Kafka automatically creates one.
   -  **context.load_verify_locations**: certificate file. This parameter is mandatory when **Security Protocol** is set to **SASL_SSL**. CRT certificates are used for accessing instances in Python.
   -  **sasl_mechanism**: SASL authentication mechanism. View it on the **Basic Information** page of the Kafka instance console. If both SCRAM-SHA-512 and PLAIN are enabled, use either of them in connection configurations. For instances that were created much earlier, if **SASL Mechanism** is not displayed on the instance details page, PLAIN is used by default.
   -  **security_protocol**: Kafka security protocol. Obtain it from the **Basic Information** page on the Kafka console. For Kafka instances that were created much earlier, if **Security Protocol** is not displayed on the instance details page, SASL_SSL is used by default.

      -  When **Security Protocol** is set to **SASL_SSL**, SASL is used for authentication. Data is encrypted with SSL certificates for high-security transmission. You need to configure the instance username, password, and certificate file.
      -  When **Security Protocol** is set to **SASL_PLAINTEXT**, SASL is used for authentication. Data is transmitted in plaintext with high performance. You need to configure the instance username and password.

-  Without SASL

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

   The parameters in the example code are described as follows. For details about how to obtain the parameter values, see :ref:`Collecting Connection Information <kafka-config>`.

   -  **bootstrap_servers**: instance connection address and port
   -  **topic_name**: topic name
   -  **consumer_id**: custom consumer group name. If the specified consumer group does not exist, Kafka automatically creates one.
