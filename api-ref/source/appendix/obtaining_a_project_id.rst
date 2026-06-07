:original_name: kafka-api-0036212547.html

.. _kafka-api-0036212547:

Obtaining a Project ID
======================

Scenario
--------

A project ID is required for some URLs when an API is called. Obtain a project ID using either of the following methods:

-  :ref:`Obtaining a Project ID by Calling an API <kafka-api-0036212547__en-us_topic_0128036884_section2871183975310>`
-  :ref:`Obtaining a Project ID on the Console <kafka-api-0036212547__en-us_topic_0128036884_section1948011550474>`

.. _kafka-api-0036212547__en-us_topic_0128036884_section2871183975310:

Obtaining a Project ID by Calling an API
----------------------------------------

You can obtain a project ID by calling the IAM API used to query projects based on specified criteria.

The API used to obtain a project ID is **GET https://**\ *{Endpoint}*\ **/v3/projects**, where *{Endpoint}* indicates the IAM endpoint. You can obtain the IAM endpoint from `Regions and Endpoints <https://docs.otc.t-systems.com/endpoint/index.html>`__.

The following is an example response. The value of **id** in the **projects** section is the project ID:

.. code-block::

   {
       "projects": [
           {
               "domain_id": "65382450e8f64ac0870cd180d14e684b",
               "is_domain": false,
               "parent_id": "65382450e8f64ac0870cd180d14e684b",
               "name": "xxx-xxx-xxx",
               "description": "",
               "links": {
                   "next": null,
                   "previous": null,
                   "self": "https://www.example.com/v3/projects/a4a5d4098fb4474fa22cd05f897d6b99"
               },
               "id": "a4a5d4098fb4474fa22cd05f897d6b99",
               "enabled": true
           }
       ],
       "links": {
           "next": null,
           "previous": null,
           "self": "https://www.example.com/v3/projects"
       }
   }

.. _kafka-api-0036212547__en-us_topic_0128036884_section1948011550474:

Obtaining a Project ID on the Console
-------------------------------------

A project ID is required for some URLs when an API is called. You can obtain a project ID on the console.

The following procedure describes how to obtain a project ID:

#. Log in to the management console.

#. Click the username and choose **My Credentials** from the drop-down list.

   On the **API Credentials** page, view project IDs in the project list.


   .. figure:: /_static/images/en-us_image_0000001862808485.png
      :alt: **Figure 1** Viewing a project ID

      **Figure 1** Viewing a project ID
