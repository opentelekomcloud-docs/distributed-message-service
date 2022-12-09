:original_name: kafka-go.html

.. _kafka-go:

Go
==

This section describes how to access a Kafka instance using Go 1.16.5 on the Linux CentOS, how to obtain the demo code, and how to produce and consume messages.

Before getting started, ensure that you have collected the information listed in :ref:`Collecting Connection Information <kafka-config>`.

Preparing the Environment
-------------------------

-  Run the following command to check whether Go has been installed:

   .. code-block::

      go version

   If the following information is displayed, Go has been installed.

   .. code-block:: console

      [root@ecs-test sarama]# go version
      go version go1.16.5 linux/amd64

   If Go is not installed, `download <https://golang.org/doc/install?download=go1.16.5.linux-amd64.tar.gz>`__ and install it.

-  Run the following command to obtain the code used in the demo:

   .. code-block::

      go get github.com/confluentinc/confluent-kafka-go/kafka

Producing Messages
------------------

.. note::

   Replace the following information in bold with the actual values.

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
          caFile   = "phy_ca.crt"     //Certificate file. For details about how to obtain an SSL certificate, see section "Collecting Connection Information."
      )

      func main() {
          log.Println("Starting a new kafka producer")

          config := &kafka.ConfigMap{
              "bootstrap.servers": brokers,
              "security.protocol": "SASL_SSL",
              "sasl.mechanism":    "PLAIN",
              "sasl.username":     user,
              "sasl.password":     password,
              "ssl.ca.location":   caFile,
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

Consuming Messages
------------------

.. note::

   Replace the following information in bold with the actual values.

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
          caFile   = "phy_ca.crt"     //Certificate file. For details about how to obtain an SSL certificate, see section "Collecting Connection Information."
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
              "ssl.ca.location":   caFile,
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
