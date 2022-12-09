:original_name: TagManagement.html

.. _TagManagement:

Managing Instance Tags
======================

Tags facilitate Kafka instance identification and management.

You can add tags to a Kafka instance when creating the instance or add tags on the **Tags** tab page of the created instance. Up to 20 tags can be added to an instance. Tags can be modified and deleted.

A tag consists of a tag key and a tag value. :ref:`Table 1 <tagmanagement__table193611920984>` lists the tag key and value requirements.

.. _tagmanagement__table193611920984:

.. table:: **Table 1** Tag key and value requirements

   +-----------------------------------+----------------------------------------------------------+
   | Parameter                         | Requirements                                             |
   +===================================+==========================================================+
   | Tag key                           | -  Cannot be left blank.                                 |
   |                                   | -  Must be unique for the same instance.                 |
   |                                   | -  Can contain a maximum of 36 characters.               |
   |                                   | -  Cannot contain the following characters: ``=*<>\,|/`` |
   |                                   | -  Cannot start or end with a space.                     |
   +-----------------------------------+----------------------------------------------------------+
   | Tag value                         | -  Cannot be left blank.                                 |
   |                                   | -  Can contain a maximum of 43 characters.               |
   |                                   | -  Cannot contain the following characters: ``=*<>\,|/`` |
   |                                   | -  Cannot start or end with a space.                     |
   +-----------------------------------+----------------------------------------------------------+

Procedure
---------

#. Log in to the management console.

#. Click |image1| in the upper left corner to select a region.

   .. note::

      Select the region where your Kafka instance is located.

#. Click **Service List** and choose **Application** > **Distributed Message Service**. The Kafka instance list is displayed.

#. Click the name of an instance.

#. Click the **Tags** tab.

   View the tags of the instance.

#. Perform the following operations as required:

   -  Add a tag

      a. Click **Add/Edit Tag**.

      b. Enter a tag key and a tag value, and click **Add**.

         If you have predefined tags, select a predefined pair of tag key and value, and click **Add**.

      c. Click **OK**.

   -  Modify a tag

      a. Click **Add/Edit Tag**.
      b. Click |image2| next to the tag to be edited, enter the original tag key and the new tag value, and click **Add**.
      c. Click **OK**.

   -  Delete a tag

      Delete a tag using either of the following methods:

      -  In the row containing the tag to be deleted, click **Delete**. In the **Delete Tag** dialog box, click **Yes**.
      -  Click **Add/Edit Tag**. In the **Add/Edit Tag** dialog box, click |image3| next to the tag to be deleted and click **OK**.

.. |image1| image:: /_static/images/en-us_image_0143929918.png
.. |image2| image:: /_static/images/en-us_image_0000001427644729.png
.. |image3| image:: /_static/images/en-us_image_0000001427644729.png
