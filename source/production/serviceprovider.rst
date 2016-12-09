.. _serviceprovider :

Service Providers
-----------------

There are 2 ways to be a Service Provider in the platform:

	* You develop and integrate your service via the Developer Cloud Sandbox [#DCS]_.
	* You or a processing center provides directly an interface to your own processing service interfacing with WPS.
	  

.. uml::
  :caption: WPS Service Providers Diagram

   !include includes/skins.iuml

   skinparam backgroundColor #FFFFFF
   skinparam componentStyle uml2

   [Portal] as portal
   () "WPS" as wps
   portal -down- wps

   [Developer Cloud Sandbox] -up-( wps

   [Processing Service] -up-( wps



With the Developer Cloud Sandbox
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Providing a processing service with the Developer Cloud Sandbox is straightforward. According to the `laboratory <http://docs.terradue.com/developer-sandbox/start/laboratory/index.html>`_ used for the service integration and the community settings on the portal, your service is automatically integrated in the Sandbox Thematic App. The Developer Cloud Sandbox exposes your application descriptor as a WPS processing. There is nothing special to do in that case except setting properly your application descriptor [#DCSAD]_.



With A Web Processing Service (WPS)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

If you provide directly a WPS via a standard interface, the platform will require the three operations that can be requested by a client and
performed by a WPS server, all mandatory implementation by all servers. Those operations are:

	- **GetCapabilities** – This operation allows the platform to request and receive back service metadata (or Capabilities) documents that describe the abilities of the specific server implementation. The GetCapabilities operation provides the names and general descriptions of each of the processes offered by a WPS instance. This operation also supports negotiation of the specification version being used for client-server interactions.

	- **DescribeProcess** – This operation allows the platform to request and receive back detailed information about the processes that can be run on the service instance, including the inputs required, their allowable formats, and the outputs that can be produced.

	- **Execute** – This operation allows the platform to run a specified process implemented by the WPS, using provided input parameter values and returning the outputs produced.


You will require only to provide the GetCapabilities endpoint url to the administrator of the platform to register it as a WPS provider.


Next sections describe the technical elements of the WPS operations that are important for the integration with the platform.


.. rubric:: Footnotes

.. [#DCS] http://docs.terradue.com/developer-sandbox/
.. [#DCSAD] http://docs.terradue.com/developer-sandbox/reference/application/index.html

