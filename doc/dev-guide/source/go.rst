:original_name: kafka-go.html

.. _kafka-go:

Go
==

This section takes Linux CentOS as an example to describe how to access a Kafka instance using a Kafka client in Go 1.16.5, including how to obtain the demo code, and produce and consume messages.

Before getting started, ensure that you have collected the information listed in :ref:`Collecting Connection Information <kafka-config>`.

Preparing the Environment
-------------------------

-  Run the following command to check whether Go has been installed:

   .. code-block::

      go version

   If the following information is displayed, Go has been installed.

   .. code-block:: console

      [root@ecs-test confluent-kafka-go]# go version
      go version go1.16.5 linux/amd64

   If Go is not installed, do as follows to install it:

   .. code-block::

      # Download the Go installation package.
      wget https://go.dev/dl/go1.16.5.linux-amd64.tar.gz

      # Decompress it to the /usr/local directory. The /usr/local directory can be changed as required.
      sudo tar -C /usr/local -xzf go1.16.5.linux-amd64.tar.gz

      # Set the environment variable.
      echo 'export PATH=$PATH:/usr/local/go/bin' >> ~/.profile
      source ~/.profile

-  Run the following command to obtain the code used in the demo:

   .. code-block::

      go get github.com/confluentinc/confluent-kafka-go/kafka

Producing Messages
------------------

-  With SASL

   .. code-block::

      package main

      import (
          "bufio"
          "fmt"
          "github.com/confluentinc/confluent-kafka-go/kafka"
          "log"
          "os"
          "os/signal"
          "syscall"
      )

      var (
          brokers  = "ip1:port1,ip2:port2,ip3:port3"
          topics   = "topic_name"
          user     = "username"
          password = "password"
          caFile   = "phy_ca.crt"     // Obtain the SSL certificate by referring to section "Collecting Connection Information". If Security Protocol is set to SASL_PLAINTEXT, delete this parameter.
      )

      func main() {
          log.Println("Starting a new kafka producer")

          config := &kafka.ConfigMap{
              "bootstrap.servers": brokers,
              "security.protocol": "SASL_SSL",
              "sasl.mechanism":    "PLAIN",
              "sasl.username":     user,
              "sasl.password":     password,
              "ssl.ca.location":   caFile,     // If Security Protocol is set to SASL_PLAINTEXT, delete this parameter.
              "ssl.endpoint.identification.algorithm": "none"
          }
          producer, err := kafka.NewProducer(config)
          if err != nil {
              log.Panicf("producer error, err: %v", err)
              return
          }

          go func() {
              for e := range producer.Events() {
                  switch ev := e.(type) {
                  case *kafka.Message:
                      if ev.TopicPartition.Error != nil {
                          log.Printf("Delivery failed: %v\n", ev.TopicPartition)
                      } else {
                          log.Printf("Delivered message to %v\n", ev.TopicPartition)
                      }
                  }
              }
          }()

          // Produce messages to topic (asynchronously)
          fmt.Println("please enter message:")
          go func() {
              for {
                  err := producer.Produce(&kafka.Message{
                      TopicPartition: kafka.TopicPartition{Topic: &topics, Partition: kafka.PartitionAny},
                      Value:          GetInput(),
                  }, nil)
                  if err != nil {
                      log.Panicf("send message fail, err: %v", err)
                      return
                  }
              }
          }()

          sigterm := make(chan os.Signal, 1)
          signal.Notify(sigterm, syscall.SIGINT, syscall.SIGTERM)
          select {
          case <-sigterm:
              log.Println("terminating: via signal")
          }
          // Wait for message deliveries before shutting down
          producer.Flush(15 * 1000)
          producer.Close()
      }

      func GetInput() []byte {
          reader := bufio.NewReader(os.Stdin)
          data, _, _ := reader.ReadLine()
          return data
      }

   The parameters in the example code are described as follows. For details about how to obtain the parameter values, see :ref:`Collecting Connection Information <kafka-config>`.

   -  **brokers**: instance connection address and port
   -  **topics**: topic name
   -  **user/password**: The username and password set when ciphertext access is enabled for the first time, or the ones set in user creation. For security purposes, you are advised to encrypt the username and password.
   -  **caFile**: certificate file This parameter is mandatory if **Security Protocol** is set to **SASL_SSL**.
   -  **security.protocol**: Kafka security protocol. Obtain it from the **Basic Information** page on the Kafka console. For Kafka instances that were created much earlier, if **Security Protocol** is not displayed on the instance details page, SASL_SSL is used by default.

      -  When **Security Protocol** is set to **SASL_SSL**, SASL is used for authentication. Data is encrypted with SSL certificates for high-security transmission. You need to configure the instance username, password, and certificate file.
      -  When **Security Protocol** is set to **SASL_PLAINTEXT**, SASL is used for authentication. Data is transmitted in plaintext with high performance. You need to configure the instance username and password.

   -  **sasl.mechanism**: SASL authentication mechanism. View it on the **Basic Information** page of the Kafka instance console. If both SCRAM-SHA-512 and PLAIN are enabled, use either of them in connection configurations. For instances that were created much earlier, if **SASL Mechanism** is not displayed on the instance details page, PLAIN is used by default.

-  Without SASL

   .. code-block::

      package main

      import (
          "bufio"
          "fmt"
          "github.com/confluentinc/confluent-kafka-go/kafka"
          "log"
          "os"
          "os/signal"
          "syscall"
      )

      var (
          brokers  = "ip1:port1,ip2:port2,ip3:port3"
          topics   = "topic_name"
      )

      func main() {
          log.Println("Starting a new kafka producer")

          config := &kafka.ConfigMap{
              "bootstrap.servers": brokers,
          }
          producer, err := kafka.NewProducer(config)
          if err != nil {
              log.Panicf("producer error, err: %v", err)
              return
          }

          go func() {
              for e := range producer.Events() {
                  switch ev := e.(type) {
                  case *kafka.Message:
                      if ev.TopicPartition.Error != nil {
                          log.Printf("Delivery failed: %v\n", ev.TopicPartition)
                      } else {
                          log.Printf("Delivered message to %v\n", ev.TopicPartition)
                      }
                  }
              }
          }()

          // Produce messages to topic (asynchronously)
          fmt.Println("please enter message:")
          go func() {
              for {
                  err := producer.Produce(&kafka.Message{
                      TopicPartition: kafka.TopicPartition{Topic: &topics, Partition: kafka.PartitionAny},
                      Value:          GetInput(),
                  }, nil)
                  if err != nil {
                      log.Panicf("send message fail, err: %v", err)
                      return
                  }
              }
          }()

          sigterm := make(chan os.Signal, 1)
          signal.Notify(sigterm, syscall.SIGINT, syscall.SIGTERM)
          select {
          case <-sigterm:
              log.Println("terminating: via signal")
          }
          // Wait for message deliveries before shutting down
          producer.Flush(15 * 1000)
          producer.Close()
      }

      func GetInput() []byte {
          reader := bufio.NewReader(os.Stdin)
          data, _, _ := reader.ReadLine()
          return data
      }

   The parameters in the example code are described as follows. For details about how to obtain the parameter values, see :ref:`Collecting Connection Information <kafka-config>`.

   -  **brokers**: instance connection address and port
   -  **topics**: topic name

Consuming Messages
------------------

-  With SASL

   .. code-block::

      package main

      import (
          "fmt"
          "github.com/confluentinc/confluent-kafka-go/kafka"
          "log"
          "os"
          "os/signal"
          "syscall"
      )

      var (
          brokers  = "ip1:port1,ip2:port2,ip3:port3"
          group    = "group-id"
          topics   = "topic_name"
          user     = "username"
          password = "password"
          caFile   = "phy_ca.crt"     // Obtain the SSL certificate by referring to section "Collecting Connection Information". If Security Protocol is set to SASL_PLAINTEXT, delete this parameter.
      )

      func main() {
          log.Println("Starting a new kafka consumer")

          config := &kafka.ConfigMap{
              "bootstrap.servers": brokers,
              "group.id":          group,
              "auto.offset.reset": "earliest",
              "security.protocol": "SASL_SSL",
              "sasl.mechanism":    "PLAIN",
              "sasl.username":     user,
              "sasl.password":     password,
              "ssl.ca.location":   caFile,     // If Security Protocol is set to SASL_PLAINTEXT, delete this parameter.
              "ssl.endpoint.identification.algorithm": "none"
          }

          consumer, err := kafka.NewConsumer(config)
          if err != nil {
              log.Panicf("Error creating consumer: %v", err)
              return
          }

          err = consumer.SubscribeTopics([]string{topics}, nil)
          if err != nil {
              log.Panicf("Error subscribe consumer: %v", err)
              return
          }

          go func() {
              for {
                  msg, err := consumer.ReadMessage(-1)
                  if err != nil {
                      log.Printf("Consumer error: %v (%v)", err, msg)
                  } else {
                      fmt.Printf("Message on %s: %s\n", msg.TopicPartition, string(msg.Value))
                  }
              }
          }()

          sigterm := make(chan os.Signal, 1)
          signal.Notify(sigterm, syscall.SIGINT, syscall.SIGTERM)
          select {
          case <-sigterm:
              log.Println("terminating: via signal")
          }
          if err = consumer.Close(); err != nil {
              log.Panicf("Error closing consumer: %v", err)
          }
      }

   The parameters in the example code are described as follows. For details about how to obtain the parameter values, see :ref:`Collecting Connection Information <kafka-config>`.

   -  **brokers**: instance connection address and port
   -  **group**: custom consumer group name. If the specified consumer group does not exist, Kafka automatically creates one.
   -  **topics**: topic name
   -  **user/password**: The username and password set when ciphertext access is enabled for the first time, or the ones set in user creation. For security purposes, you are advised to encrypt the username and password.
   -  **caFile**: certificate file This parameter is mandatory if **Security Protocol** is set to **SASL_SSL**.
   -  **security.protocol**: Kafka security protocol. Obtain it from the **Basic Information** page on the Kafka console. For Kafka instances that were created much earlier, if **Security Protocol** is not displayed on the instance details page, SASL_SSL is used by default.

      -  When **Security Protocol** is set to **SASL_SSL**, SASL is used for authentication. Data is encrypted with SSL certificates for high-security transmission. You need to configure the instance username, password, and certificate file.
      -  When **Security Protocol** is set to **SASL_PLAINTEXT**, SASL is used for authentication. Data is transmitted in plaintext with high performance. You need to configure the instance username and password.

   -  **sasl.mechanism**: SASL authentication mechanism. View it on the **Basic Information** page of the Kafka instance console. If both SCRAM-SHA-512 and PLAIN are enabled, use either of them in connection configurations. For instances that were created much earlier, if **SASL Mechanism** is not displayed on the instance details page, PLAIN is used by default.

-  Without SASL

   .. code-block::

      package main

      import (
          "fmt"
          "github.com/confluentinc/confluent-kafka-go/kafka"
          "log"
          "os"
          "os/signal"
          "syscall"
      )

      var (
          brokers  = "ip1:port1,ip2:port2,ip3:port3"
          group    = "group-id"
          topics   = "topic_name"
      )

      func main() {
          log.Println("Starting a new kafka consumer")

          config := &kafka.ConfigMap{
              "bootstrap.servers": brokers,
              "group.id":          group,
              "auto.offset.reset": "earliest",
          }

          consumer, err := kafka.NewConsumer(config)
          if err != nil {
              log.Panicf("Error creating consumer: %v", err)
              return
          }

          err = consumer.SubscribeTopics([]string{topics}, nil)
          if err != nil {
              log.Panicf("Error subscribe consumer: %v", err)
              return
          }

          go func() {
              for {
                  msg, err := consumer.ReadMessage(-1)
                  if err != nil {
                      log.Printf("Consumer error: %v (%v)", err, msg)
                  } else {
                      fmt.Printf("Message on %s: %s\n", msg.TopicPartition, string(msg.Value))
                  }
              }
          }()

          sigterm := make(chan os.Signal, 1)
          signal.Notify(sigterm, syscall.SIGINT, syscall.SIGTERM)
          select {
          case <-sigterm:
              log.Println("terminating: via signal")
          }
          if err = consumer.Close(); err != nil {
              log.Panicf("Error closing consumer: %v", err)
          }
      }

   The parameters in the example code are described as follows. For details about how to obtain the parameter values, see :ref:`Collecting Connection Information <kafka-config>`.

   -  **brokers**: instance connection address and port
   -  **group**: custom consumer group name. If the specified consumer group does not exist, Kafka automatically creates one.
   -  **topics**: topic name
