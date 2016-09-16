Execution
~~~~~~~~~

WPS Execute
===========

The webserver offers an Execute service, requesting the execution of a job for a given WPS service.

.. code-block:: http

    POST t2api/wps/WebProcessingService?service=wps&request=Execute&version=<serviceVersion>&identifier=<service_identifier>

The body of the request must contain an WPS Execute object in the application/xml format.

.. code-block:: xml
	
	<wps:Execute service="WPS" version="1.0.0" xmlns="http://www.opengis.net/wps/1.0.0" xmlns:gml="http://www.opengis.net/gml" xmlns:ogc="http://www.opengis.net/ogc" xmlns:ows="http://www.opengis.net/ows/1.1" xmlns:wcs="http://www.opengis.net/wcs/1.1.1" xmlns:wfs="http://www.opengis.net/wfs" xmlns:wps="http://www.opengis.net/wps/1.0.0" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://www.opengis.net/wps/1.0.0 http://schemas.opengis.net/wps/1.0.0/wpsAll.xsd">
		<ows:Identifier>e748c24b-fr3e-48cb-a4a4-904d30fadc20</ows:Identifier>
		<wps:DataInputs>
			<wps:Input>
				<ows:Identifier>slave</ows:Identifier>
				<wps:Data>
					<wps:LiteralData><![CDATA[http://eo-virtual-archive4.esa.int/search/ASA_IMS_1P/ASA_IMS_1PNDPA20080326_204749_000000162067_00129_31746_3124.N1/rdf]]></wps:LiteralData>
				</wps:Data>
			</wps:Input>
			<wps:Input>
				<ows:Identifier>poi</ows:Identifier>
				<wps:Data>
					<wps:LiteralData><![CDATA[POINT(13.4 42.35)]]></wps:LiteralData>
				</wps:Data>
			</wps:Input>
			<wps:Input>
				<ows:Identifier>extent</ows:Identifier>
				<wps:Data>
					<wps:LiteralData><![CDATA[2000,2000]]></wps:LiteralData>
				</wps:Data>
			</wps:Input>
			<wps:Input>
				<ows:Identifier>settings</ows:Identifier>
				<wps:Data>
					<wps:LiteralData><![CDATA[cc_winsize=&quot;128 128&quot;,fc_acc=&quot;8 8&quot;,int_multilook=&quot;4 4&quot;,coh_multilook=&quot;4 4&quot;,dumpbaseline=&quot;15 10&quot;]]></wps:LiteralData>
				</wps:Data>
			</wps:Input>
			<wps:Input>
				<ows:Identifier>master</ows:Identifier>
				<wps:Data>
					<wps:LiteralData><![CDATA[http://eo-virtual-archive4.esa.int/search/ASA_IMS_1P/ASA_IMS_1PNDPA20090311_204746_000000162077_00129_36756_3125.N1/rdf]]></wps:LiteralData>
				</wps:Data>
			</wps:Input>
		</wps:DataInputs>
		<wps:ResponseForm>
			<wps:ResponseDocument status="true" storeExecuteResponse="true">
				<wps:Output mimeType="application/xml">
					<ows:Identifier>result_osd</ows:Identifier>
				</wps:Output>
				<wps:Output mimeType="application/xml">
					<ows:Identifier>result_distribution</ows:Identifier>
				</wps:Output>
			</wps:ResponseDocument>
		</wps:ResponseForm>
	</wps:Execute>



The webserver acts as a proxy for all Web Processing Services added by the Administrator of the Portal.
He forward the Execute request to the WPS and returns the ExecuteResponse. The response is conform to the WPS standard defined by OGC (http://schemas.opengis.net/wps/1.0.0).

.. code-block:: xml

	<?xml version="1.0" encoding="us-ascii"?>
	<ExecuteResponse xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" service="WPS" version="1.0.0" xml:lang="en-US" serviceInstance="https://geohazards-tep.eo.esa.int/t2api/wps/WebProcessingService?REQUEST=GetCapabilities&amp;SERVICE=WPS" statusLocation="https://geohazards-tep.eo.esa.int/t2api/wps/RetrieveResultServlet?id=049f5c6w-6e45-4808-8397-0a8b89d9a56f" xmlns="http://www.opengis.net/wps/1.0.0">
	  <Process d2p1:processVersion="1.0.0" xmlns:d2p1="http://www.opengis.net/wps/1.0.0">
	    <Identifier xmlns="http://www.opengis.net/ows/1.1">com.terradue.wps_oozie.process.OozieAbstractAlgorithm</Identifier>
	    <Title xmlns="http://www.opengis.net/ows/1.1">ADORE DORIS interferometric processor</Title>
	  </Process>
	  <Status creationTime="2016-09-16T10:05:40.641+02:00">
	    <ProcessAccepted>Process Accepted</ProcessAccepted>
	  </Status>
	  <DataInputs />
	  <OutputDefinitions />
	  <ProcessOutputs />
	</ExecuteResponse>

Get Job Status
==============

The webserver offers a GetStatus service, requesting the status of an existing job ran on the platform.

.. code-block:: http

    GET t2api/wps/RetrieveResultServlet?id=<job_id>

The webserver acts as a proxy for all Web Processing Services added by the Administrator of the Portal.
He forward the GetStatus request to the WPS and returns the ExecuteResponse. The response is conform to the WPS standard defined by OGC (http://schemas.opengis.net/wps/1.0.0).

.. code-block:: xml

	<?xml version="1.0" encoding="us-ascii"?>
	<ExecuteResponse xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" service="WPS" version="1.0.0" xml:lang="en-US" serviceInstance="https://geohazards-tep.eo.esa.int/t2api/wps/WebProcessingService?REQUEST=GetCapabilities&amp;SERVICE=WPS" statusLocation="https://geohazards-tep.eo.esa.int/t2api/wps/RetrieveResultServlet?id=049f5c6w-6e45-4808-8397-0a8b89d9a56f" xmlns="http://www.opengis.net/wps/1.0.0">
	  <Process d2p1:processVersion="1.0.0" xmlns:d2p1="http://www.opengis.net/wps/1.0.0">
	    <Identifier xmlns="http://www.opengis.net/ows/1.1">com.terradue.wps_oozie.process.OozieAbstractAlgorithm</Identifier>
	    <Title xmlns="http://www.opengis.net/ows/1.1">ADORE DORIS interferometric processor</Title>
	  </Process>
	  <Status creationTime="2016-09-16T10:05:40.641+02:00">
	    <ProcessStarted percentCompleted="33" />
	  </Status>
	  <DataInputs />
	  <OutputDefinitions />
	  <ProcessOutputs />
	</ExecuteResponse>
