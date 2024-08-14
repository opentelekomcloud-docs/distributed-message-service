:original_name: kafka-ug-180418002.html

.. _kafka-ug-180418002:

Viewing Kafka Audit Logs
========================

With Cloud Trace Service (CTS), you can record operations associated with DMS for later query, audit, and backtrack operations.

Prerequisite
------------

CTS has been enabled.

DMS Operations Supported by CTS
-------------------------------

.. table:: **Table 1** DMS operations that can be recorded by CTS

   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Operation                                                                 | Resource Type | Trace Name                             |
   +===========================================================================+===============+========================================+
   | Successfully creating an instance                                         | kafka         | createDMSInstanceTaskSuccess           |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Failing to create an instance                                             | kafka         | createDMSInstanceTaskFailure           |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Successfully deleting an instance that failed to be created               | kafka         | deleteDMSCreateFailureInstancesSuccess |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Failing to delete an instance that failed to be created                   | kafka         | deleteDMSCreateFailureInstancesFailure |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Successfully deleting an instance                                         | kafka         | deleteDMSInstanceTaskSuccess           |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Failing to delete an instance                                             | kafka         | deleteDMSInstanceTaskFailure           |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Deleting multiple instance tasks at a time                                | kafka         | batchDeleteDMSInstanceTask             |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Successfully submitting a request to delete multiple instances at a time  | kafka         | batchDeleteDMSInstanceSuccess          |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Successfully deleting multiple instances at a time                        | kafka         | batchDeleteDMSInstanceTaskSuccess      |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Failing to submit a request to delete multiple instances at a time        | kafka         | batchDeleteDMSInstanceFailure          |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Failing to delete multiple instances at a time                            | kafka         | batchDeleteDMSInstanceTaskFailure      |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Successfully submitting a request to scale up an instance                 | kafka         | extendDMSInstanceSuccess               |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Successfully scaling up an instance                                       | kafka         | extendDMSInstanceTaskSuccess           |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Failing to submit a request to scale up an instance                       | kafka         | extendDMSInstanceFailure               |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Failing to scale up an instance                                           | kafka         | extendDMSInstanceTaskFailure           |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Successfully submitting a request to reset instance password              | kafka         | resetDMSInstancePasswordSuccess        |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Failing to submit a request to reset instance password                    | kafka         | resetDMSInstancePasswordFailure        |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Successfully submitting a request to restart an instance                  | kafka         | restartDMSInstanceSuccess              |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Successfully restarting an instance                                       | kafka         | restartDMSInstanceTaskSuccess          |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Failing to submit a request to restart an instance                        | kafka         | restartDMSInstanceFailure              |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Failing to restart an instance                                            | kafka         | restartDMSInstanceTaskFailure          |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Successfully submitting a request to restart multiple instances at a time | instance      | batchRestartDMSInstanceSuccess         |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Successfully restarting multiple instances at a time                      | kafka         | batchRestartDMSInstanceTaskSuccess     |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Failing to submit a request to restart multiple instances at a time       | instance      | batchRestartDMSInstanceFailure         |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Failing to restart multiple instances at a time                           | kafka         | batchRestartDMSInstanceTaskFailure     |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Successfully submitting a request to modify instance information          | kafka         | modifyDMSInstanceInfoSuccess           |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Successfully modifying instance information                               | kafka         | modifyDMSInstanceInfoTaskSuccess       |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Failing to submit a request to modify instance information                | kafka         | modifyDMSInstanceInfoFailure           |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Failing to modify instance information                                    | kafka         | modifyDMSInstanceInfoTaskFailure       |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Successfully deleting a background task                                   | kafka         | deleteDMSBackendJobSuccess             |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Failing to delete a background task                                       | kafka         | deleteDMSBackendJobFailure             |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Successfully enabling Smart Connect                                       | kafka         | createConnectorTaskSuccess             |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Successfully creating a Smart Connect task                                | kafka         | createConnectorSinkTaskSuccess         |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Failing to enable Smart Connect                                           | kafka         | createConnectorTaskFailure             |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Failing to create a Smart Connect task                                    | kafka         | createConnectorSinkTaskFailure         |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Successfully creating a topic for a Kafka instance                        | kafka         | Kafka_create_topicSuccess              |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Failing to create a topic for a Kafka instance                            | kafka         | Kafka_create_topicFailure              |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Successfully deleting a topic from a Kafka instance                       | kafka         | Kafka_delete_topicsSuccess             |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Failing to delete a topic for a Kafka instance                            | kafka         | Kafka_delete_topicsFailure             |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Successfully enabling automatic topic creation                            | kafka         | enable_auto_topicSuccess               |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Failing to enable automatic topic creation                                | kafka         | enable_auto_topicFailure               |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Successfully modifying a topic                                            | kafka         | Kafka_alter_topicsSuccess              |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Failing to modify a topic                                                 | kafka         | Kafka_alter_topicsFailure              |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Successfully reassigning partitions                                       | kafka         | kafka_reassignmentTaskSuccess          |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Failing to reassign partitions                                            | kafka         | kafka_reassignmentTaskFailure          |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Successfully submitting a partition reassignment request                  | kafka         | kafka_reassignmentSuccess              |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Failing to submit a partition reassignment request                        | kafka         | kafka_reassignmentFailure              |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Successfully resetting the consumer offset                                | kafka         | Kafka_reset_consumer_offsetSuccess     |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Failing to reset the consumer offset                                      | kafka         | Kafka_reset_consumer_offsetFailure     |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Successfully deleting consumer groups in batches                          | kafka         | Kafka_batch_delete_groupSuccess        |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Failing to delete consumer groups in batches                              | kafka         | Kafka_batch_delete_groupFailure        |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Successfully creating a user                                              | kafka         | createUserSuccess                      |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Failing to create a user                                                  | kafka         | createUserFailure                      |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Successfully deleting a user                                              | kafka         | deleteUserSuccess                      |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Failing to delete a user                                                  | kafka         | deleteUserFailure                      |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Successfully updating user policies                                       | kafka         | updateUserPoliciesTaskSuccess          |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+
   | Failing to update user policies                                           | kafka         | updateUserPoliciesTaskFailure          |
   +---------------------------------------------------------------------------+---------------+----------------------------------------+

Viewing Audit Logs
------------------

See `Querying Real-Time Traces <https://docs.otc.t-systems.com/en-us/usermanual/cts/en-us_topic_0030598499.html>`__.
