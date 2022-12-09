:original_name: kafka-ug-180418003.html

.. _kafka-ug-180418003:

Viewing Audit Logs
==================

Scenario
--------

This section describes how to view operation records of the last 7 days on the CTS console.

Procedure
---------

#. Log in to the management console.

#. Click |image1| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Management & Deployment** > **Cloud Trace Service**.

#. In the navigation pane, choose **Trace List**.

#. Set filters to search for desired traces. The following filters are available:

   -  **Trace Source**: Select **DMS**.
   -  **Resource Type**: Select **kafka** or **Instance**.
   -  **Search By**: Select an option from the drop-down list.

      -  When you select **Trace name**, you also need to select a specific :ref:`trace name <kafka-ug-180418002__table17570937171914>`.
      -  If you select **Resource ID** for **Search By**, you need to enter a specific resource ID. The corresponding operation trace can be queried only when the resource ID is completely matched.
      -  When you select **Resource name**, you also need to select a specific resource name.

   -  **Operator**: Select a specific operator (a user other than tenant).
   -  **Trace Status**: Available options include **All trace statuses**, **normal**, **warning**, and **incident**. You can only select one of them.
   -  **Time Range**: In the upper right corner, choose **Last 1 hour**, **Last 1 day**, or **Last 1 week**, or specify a custom time range. If you select **Customize**, you also need to select the start time and end time, and then click **OK**.

#. Click |image2| on the left of a trace to expand its details.


   .. figure:: /_static/images/en-us_image_0000001330112650.png
      :alt: **Figure 1** Expanding trace details

      **Figure 1** Expanding trace details

#. Click **View Trace** in the **Operation** column. In the dialog box, the trace details are displayed, as shown in :ref:`Figure 2 <kafka-ug-180418003__fig1620891412115>`.

   .. _kafka-ug-180418003__fig1620891412115:

   .. figure:: /_static/images/en-us_image_0000001329793006.png
      :alt: **Figure 2** Viewing a trace

      **Figure 2** Viewing a trace

.. |image1| image:: /_static/images/en-us_image_0143929918.png
.. |image2| image:: /_static/images/en-us_image_0000001160594580.png
