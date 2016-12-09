.. _usingwps :

Using Web Processing Service
----------------------------

The webserver acts as a boker and proxy for all Web Processing Services integrated in the platform.
He gathers all GetCapabilities of all WPS registered and returns this as an aggregated GetCapabilities response. The response is conform to the WPS standard defined by OGC (http://schemas.opengis.net/wps/1.0.0).

GetCapabilities
^^^^^^^^^^^^^^^

The portal API exposes a GetCapabilites service, describing all Web Processing Services accessible by the current logged user.

.. code-block:: http

    GET <portal_baseurl>/t2api/wps/WebProcessingService?service=wps&request=GetCapabilities


DescribeProcess
^^^^^^^^^^^^^^^

At next level the portal API exposes a DescribeProcess service, describing a given WPS service.

.. code-block:: http

    GET <portal_baseurl>/t2api/wps/WebProcessingService?service=wps&request=DescribeProcess&version=<serviceVersion>&identifier=<service_identifier>

Execute
^^^^^^^

Finally, the portal API implements the Execute service, requesting the execution of a job for a given WPS service.

.. code-block:: http

    POST <portal_baseurl>/t2api/wps/WebProcessingService?service=wps&request=Execute&version=<serviceVersion>&identifier=<service_identifier>

Altough depending on the WPS implementation, if the WPS provider follows correctly the guideline descried :ref:`here <providingwps>` the Execute Response shall return a statusLocation URL that can be polled to query the status of the execution.

Once completed the same URL shall return all the information to retrieve the results.

RetrieveResults
^^^^^^^^^^^^^^^

The portal API will return the results received from the proxy WPS Execute Response. It will analyze the outputs to provide with an :ref:`OpenSearch <opensearch>` service to query and get results in a standard way.


OpenSearch Description Document
"""""""""""""""""""""""""""""""

If the analysis of the results allows it, the response contains one `Output` element identified `result_osd` with a Reference URL pointing to an OpenSearch Description.

.. code-block:: xml
	<?xml version="1.0" encoding="us-ascii"?>
	<wps:Output>
		<ows:Identifier xmlns:ns1="http://www.opengis.net/ows/1.1">result_osd</ows:Identifier>
		<ows:Title xmlns:ns1="http://www.opengis.net/ows/1.1">OpenSearch Description to the Results</ows:Title>
			<wps:Reference href="https://tep-geohazards-dev.terradue.com/t2api/proxy?url=http%3a%2f%2fsb-10-16-10-20.dev.terradue.int%2fsbws%2fwps%2fdcs-doris-ifg%2f0000023-160501000006641-oozie-oozi-W%2fresults%2fdescription" mimeType="application/opensearchdescription+xml" />
	</wps:Output> 



.. rubric:: Footnotes

.. [#DCS] http://docs.terradue.com/developer-sandbox/
.. [#DCSAD] http://docs.terradue.com/developer-sandbox/reference/application/index.html

