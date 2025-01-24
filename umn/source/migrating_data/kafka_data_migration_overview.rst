:original_name: kafka-bp-migration.html

.. _kafka-bp-migration:

Kafka Data Migration Overview
=============================

You can migrate Kafka services to connect message producers and consumers to a new Kafka instance and can even migrate persisted message data to the new Kafka instance. Kafka services can be migrated in the following two scenarios:

-  Migrating services to the cloud without downtime

   Services that have high requirements on continuity must be smoothly migrated to the cloud because they cannot afford a long downtime.

-  Re-deploying services on the cloud

   A Kafka instance deployed within an AZ is not capable of cross-AZ disaster recovery. For higher reliability, you can re-deploy services to an instance that is deployed across AZs.

Constraints
-----------

-  When Smart Connect is used to migrate services, it consumes the source Kafka messages and produces messages to the target Kafka instance, occupying the bandwidth of the source and the target Kafka.
-  To maintain performance, Smart Connect only synchronizes the source and target data in real time. The consumption progress is synchronized in batches, so the consumption progress on the source and target partitions may vary from 0 to 100.

Preparation
-----------

#. Configure the network environment.

   A Kafka instance can be accessed within a VPC or over a public network. For public network access, the producer and consumer must have public access permissions, and the following security group rules must be configured.

   .. table:: **Table 1** Security group rules

      +-----------+----------+------+-----------+----------------------------------------------------------------+
      | Direction | Protocol | Port | Source    | Description                                                    |
      +===========+==========+======+===========+================================================================+
      | Inbound   | TCP      | 9094 | 0.0.0.0/0 | Accessing a Kafka instance in a public network (in plaintext)  |
      +-----------+----------+------+-----------+----------------------------------------------------------------+
      | Inbound   | TCP      | 9095 | 0.0.0.0/0 | Accessing a Kafka instance in a public network (in ciphertext) |
      +-----------+----------+------+-----------+----------------------------------------------------------------+

#. Create the target Kafka instance.

   The specifications of the target instance cannot be lower than the original specifications. For more information, see :ref:`Creating a Kafka Instance <kafka-ug-180604013>`.

#. Create a topic in the target Kafka instance.

   Create a topic with the same configurations as the original Kafka instance, including the topic name, number of replicas, number of partitions, message aging time, and whether to enable synchronous replication and flushing. For more information, see :ref:`Creating a Kafka Topic <kafka-ug-180604018>`.

Migration Scheme 1: Migrating the Production First
--------------------------------------------------

Migrate the message production service to the new Kafka instance. After migration, the original Kafka instance will no longer produce messages. After all messages of the original Kafka instance are consumed, migrate the message consumption service to the new Kafka instance to consume messages of this instance.

This is a common migration scheme. It is simple and easy to control on the service side. During the migration, the message sequence is ensured, so this scheme is **suitable for scenarios with strict requirements on the message sequence**. However, latency may occur because there is a period when you have to wait for all data to be consumed.

#. Change the Kafka connection address of the producer to that of the new Kafka instance.

#. Restart the production service so that the producer can send new messages to the new Kafka instance.

#. .. _kafka-bp-migration__li1925613325914:

   Check the consumption progress of each consumer group in the original Kafka instance until all data in the original Kafka instance is consumed.

#. Change the Kafka connection addresses of the consumers to those of the new Kafka instance.

#. Restart the consumption service so that consumers can consume messages from the new Kafka instance.

#. Check whether consumers consume messages properly from the new Kafka instance.

#. The migration is complete.

Migration Scheme 2: Migrating the Production Later
--------------------------------------------------

Use multiple consumers for the consumption service. Some consume messages from the original Kafka instance, and others consume messages from the new Kafka instances. Then, migrate the production service to the new Kafka instance so that all messages can be consumed in time.

For a certain period of time, the consumption service consumes messages from both the original and new Kafka instances. Before the migration, message consumption from the new Kafka instance has already started, so there is no latency. However, early on in the migration, data is consumed from both the original and new Kafka instances, so the messages may not be consumed in the order that they are produced. This scheme is **suitable for services that require low latency but do not require strict message sequence**.

#. Start new consumer clients, set the Kafka connection addresses to that of the new Kafka instance, and consume data from the new Kafka instance.

   .. note::

      Original consumer clients must continue running. Messages are consumed from both the original and new Kafka instances.

#. Change the Kafka connection address of the producer to that of the new Kafka instance.
#. Restart the producer client to migrate the production service to the new Kafka instance.
#. After the production service is migrated, check whether the consumption service connected to the new Kafka instance is normal.
#. After all data in the original Kafka is consumed, close the original consumption clients.
#. The migration is complete.

Migration Scheme 3: Migrating the Consumption First
---------------------------------------------------

Use Smart Connect to synchronize the two Kafka instances, migrate the consumer first and then the producer to the new Kafka instance.

This scheme uses Smart Connect to synchronize the source and target data in real time. However, the consumption progress is synchronized in batches. The consumption progress on the source and target partition may vary from 0 to 100. As a result, some messages are repeatedly consumed. This scheme applies to services where the message production must continue, end-to-end latency must be low, and repeated consumption can be tolerated.

#. Create a Smart Connect task for Kafka data replication. For details, see :ref:`Replicating Kafka Instance Data <kafka-ug-0034>`.
#. On the **Message Query** page of the Kafka console, check whether the latest messages and the synchronization progress of both Kafka instances are consistent. For details, see :ref:`Viewing Kafka Messages <kafka-ug-190904001>`.

   -  Yes: Go to :ref:`3 <kafka-bp-migration__li1925613325914>`.
   -  No: Check whether the synchronized data per minute of both Kafka instances is normal. If yes, wait for the synchronization progress of both Kafka instances to be consistent, then go to :ref:`3 <kafka-bp-migration__li1925613325914>`.

#. Change the Kafka connection addresses of the consumers to those of the new Kafka instance.
#. Restart the consumption service so that consumers can consume messages from the new Kafka instance.
#. Check whether consumers consume messages properly from the new Kafka instance.
#. Change the Kafka connection address of the producer to that of the new Kafka instance.
#. Restart the producer client to migrate the production service to the new Kafka instance.
#. After the production service is migrated, check whether the consumption service connected to the new Kafka instance is normal.
#. The migration is complete.

How Do I Migrate Persisted Data Along with Services?
----------------------------------------------------

You can migrate consumed data from the original instance to a new instance by using Smart Connect. This tool mirrors the original Kafka producer and consumer into new ones and migrates data to the new Kafka instance. For details, see :ref:`Replicating Kafka Instance Data <kafka-ug-0034>`.

Note that each cloud Kafka instance stores data in three replicas. Therefore, the storage space of the new instance should be three times that of the original single-replica message storage.
