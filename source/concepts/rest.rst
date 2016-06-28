REST api
--------

All the commands described in the following sections are provided using the comprehensive HTTP REST API of the platform.

Usage
^^^^^

Platform's REST API endpoints can be invoked in any of the standard ways to invoke a RESTful API. Most of the following sections describe how to use the REST API using ``cURL`` or ``opensearch-client`` as an example.

.. note:: Using and Configuring cURL
  You can download cURL `here <http://curl.haxx.se/download.html>`_. Learn how to use and configure cURL `here <http://curl.haxx.se/docs/manpage.html>`_.


Authentication
^^^^^^^^^^^^^^

One of most important parameter to set in those REST commands is your API key which is configured in your profile page in the portal.

REST API supports three forms of authentication:

 - Basic authentication using your username and password.
 - Basic authentication using your username and API Key.
 - Using a dedicated header (e.g. ``X-T2-Api``) with your API Key.
   


Routes
^^^^^^

Routes are semantically important, especially in the case of searching.

.. code-block:: console

    https://data.terradue.com/catalogue/mrossi/geotime/search
    `---------------------------------´`-------------´`-----´
                    |                         |          |
              service base url            resource   operation


The operation part can also be absent and the HTTP verb defines it. (e.g. PUT for update)

the following paragraphs summarize the different types of route of the platform

Data Agency - Catalogue service
'''''''''''''''''''''''''''''''

.. code-block:: console

    https://data.terradue.com/catalogue/<indexName>/<type>[/<operation>]


Data Agency - Storage service
'''''''''''''''''''''''''''''

.. code-block:: console

    https://data.terradue.com/storage/<repoName>[/<folder>]/<file>.<ext>

    



