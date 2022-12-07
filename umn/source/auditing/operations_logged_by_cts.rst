:original_name: kafka-ug-180418002.html

.. _kafka-ug-180418002:

Operations Logged by CTS
========================

With Cloud Trace Service (CTS), you can record operations associated with DMS for later query, audit, and backtrack operations.

.. _kafka-ug-180418002__table17570937171914:

.. table:: **Table 1** DMS operations that can be recorded by CTS

   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Operation                                                                 | Resource Type | Trace Name                             |
   +===========================================================================+===============+========================================+
   | Successfully deleting a background task                                   | kafka         | deleteDMSBackendJobSuccess             |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Failing to delete a background task                                       | kafka         | deleteDMSBackendJobFailure             |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Successfully creating an order for creating an instance                   | kafka         | createDMSInstanceOrderSuccess          |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Failing to create an order for creating an instance                       | kafka         | createDMSInstanceOrderFailure          |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Successfully submitting a request to modify an instance order             | kafka         | modifyDMSInstanceOrderSuccess          |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Failing to submit a request to modify an instance order                   | kafka         | modifyDMSInstanceOrderFailure          |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Successfully submitting a request to scale up an instance                 | kafka         | extendDMSInstanceSuccess               |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Failing to submit a request to scale up an instance                       | kafka         | extendDMSInstanceFailure               |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Successfully submitting a request to reset instance password              | kafka         | resetDMSInstancePasswordSuccess        |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Failing to submit a request to reset instance password                    | kafka         | resetDMSInstancePasswordFailure        |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Successfully creating a topic for a Kafka instance                        | kafka         | Kafka_platinum_create_topicSuccess     |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Failing to create a topic for a Kafka instance                            | kafka         | Kafka_platinum_create_topicFailure     |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Successfully deleting a topic from a Kafka instance                       | kafka         | Kafka_platinum_delete_topicsSuccess    |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Failing to delete a topic for a Kafka instance                            | kafka         | Kafka_platinum_delete_topicsFailure    |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Successfully deleting an instance that failed to be created               | kafka         | deleteDMSCreateFailureInstancesSuccess |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Failing to delete an instance that failed to be created                   | kafka         | deleteDMSCreateFailureInstancesFailure |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Successfully submitting a request to restart an instance                  | kafka         | restartDMSInstanceSuccess              |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Failing to submit a request to restart an instance                        | kafka         | restartDMSInstanceFailure              |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Successfully submitting a request to delete multiple instances at a time  | kafka         | batchDeleteDMSInstanceSuccess          |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Failing to submit a request to delete multiple instances at a time        | kafka         | batchDeleteDMSInstanceFailure          |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Successfully submitting a request to restart multiple instances at a time | kafka         | batchRestartDMSInstanceSuccess         |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Failing to submit a request to restart multiple instances at a time       | kafka         | batchRestartDMSInstanceFailure         |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Successfully submitting a request to modify instance information          | kafka         | modifyDMSInstanceInfoSuccess           |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Failing to submit a request to modify instance information                | kafka         | modifyDMSInstanceInfoFailure           |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Deleting multiple instance tasks at a time                                | kafka         | batchDeleteDMSInstanceTask             |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Successfully deleting an instance                                         | kafka         | deleteDMSInstanceTaskSuccess           |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Failing to delete an instance                                             | kafka         | deleteDMSInstanceTaskFailure           |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Successfully creating an instance                                         | kafka         | createDMSInstanceTaskSuccess           |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Failing to create an instance                                             | kafka         | createDMSInstanceTaskFailure           |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Successfully scaling up an instance                                       | kafka         | extendDMSInstanceTaskSuccess           |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Failing to scale up an instance                                           | kafka         | extendDMSInstanceTaskFailure           |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Successfully restarting an instance                                       | kafka         | restartDMSInstanceTaskSuccess          |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Failing to restart an instance                                            | kafka         | restartDMSInstanceTaskFailure          |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Successfully restarting multiple instances at a time                      | kafka         | batchRestartDMSInstanceTaskSuccess     |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Failing to restart multiple instances at a time                           | kafka         | batchRestartDMSInstanceTaskFailure     |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Successfully modifying instance information                               | kafka         | modifyDMSInstanceInfoTaskSuccess       |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Failing to modify instance information                                    | kafka         | modifyDMSInstanceInfoTaskFailure       |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
