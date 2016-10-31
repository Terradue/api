.. _providingwps :

Providing Web Processing Service
--------------------------------

In order to provide an elligible Web Processing Service to the platform, we describe herafter the 3 basic operations that must be implmented. We will not detail them since they are already fully specific in the OGC standard [#OGCWPS]_ but we will underlign some aspects of the content that are important for a successful integration into the platform.


Proxy or not proxy?
^^^^^^^^^^^^^^^^^^^

The platform can integrate the WPS in 2 modes, with the request proxied by the platform of the service exposed directly to the user. If you choose to integrate your WPS not proxied, the user client such as the web browser (via the portal application) will have access to you endpoint without intermediary. It is themn up to your system to control the access to it.

When you choose your WPS to be proxied, all the HTTP request between the user and your system are passed via the platform. This option has the following additional possibilities:

System credentials
""""""""""""""""""

You can protect your system with a system username and password. Those credentials will never be divulgated to the user but only used by the platform when making the HTTP requests to your system. When registering your service, just include your username and password to the GetCapabilities URL and it will be then reused for any further request on the same domain of the WPS provider.

.. code-block:: console

    http://system:secret@wps.comany.com/wps?service=WPS&version=1.0.0&request=GetCapabilities


User Identification
"""""""""""""""""""

In order to be able to identify the user making the request on your WPS system for accounting of control access purposes, the platform include an HTTP header with information about the user and the context in which he initiated the request. Here are those headers:

+---------------+--------+--------------------------------------------------------------------+
| Header Name   | Type   | Description                                                        |
+===============+========+====================================================================+
| REMOTE_USER   | string | username of the user in the platform (unique)                      |
+---------------+--------+--------------------------------------------------------------------+
| REMOTE_DOMAIN | string | :ref:`domain` for which the user has instantiated the request      |
+---------------+--------+--------------------------------------------------------------------+
| REMOTE_ROLE   | string | :ref:`role` of the user in the domain in which he made the request |
+---------------+--------+--------------------------------------------------------------------+



GetCapabilities Operation
^^^^^^^^^^^^^^^^^^^^^^^^^

The WPS provider must provide with a GetCapabilites service, presenting all Web Processing Services accessible.

.. code-block:: http

    GET .../<WebProcessingService>?service=wps&request=GetCapabilities



DescribeProcess Operation
^^^^^^^^^^^^^^^^^^^^^^^^^

For each process listed in the GetCapabilities, the WPS have to provide a proper WPS DescribeProcess interface.

.. code-block:: http

    GET .../<WebProcessingService>?service=wps&request=DescribeProcess&version=<serviceVersion>&identifier=<service_identifier>



.. rubric:: Footnotes

.. [#OGCWPS] http://www.opengeospatial.org/standards/wps

