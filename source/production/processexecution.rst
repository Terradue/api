.. _processexecution :

Process Execution
-----------------

This operation of the WPS is probably the most important one, especially for the input and output format and defintion that requires some specific elements to be properly integrated with the platform.


.. _processexecuteoperation :

Execute Operation
^^^^^^^^^^^^^^^^^
	
The WPS service must implement the execute interface with the submission of parameters in HTTP POST.

.. code-block:: http

    POST ../<WebProcessingService>?service=wps&request=Execute&version=<serviceVersion>&identifier=<service_identifier>

The body of the request must contain an WPS Execute object in the application/xml format.


Job Status
""""""""""

The platform supports both synchronous or asynchronous request. In the latter case, the platform will poll the statusLocation of the ExecuteResponse until the job is completed.

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


For instance, it will poll such an URL


.. code-block:: http

    GET .../<RetrieveResultServlet>?id=<job_id>



that could return a process status started with 33% completed:

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


When completed


.. code-block:: xml

	<?xml version="1.0" encoding="us-ascii"?>
	<ExecuteResponse xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" service="WPS" version="1.0.0" xml:lang="en-US" serviceInstance="https://geohazards-tep.eo.esa.int/t2api/wps/WebProcessingService?REQUEST=GetCapabilities&amp;SERVICE=WPS" statusLocation="https://geohazards-tep.eo.esa.int/t2api/wps/RetrieveResultServlet?id=049f5c6w-6e45-4808-8397-0a8b89d9a56f" xmlns="http://www.opengis.net/wps/1.0.0">
	  <Process d2p1:processVersion="1.0.0" xmlns:d2p1="http://www.opengis.net/wps/1.0.0">
	    <Identifier xmlns="http://www.opengis.net/ows/1.1">com.terradue.wps_oozie.process.OozieAbstractAlgorithm</Identifier>
	    <Title xmlns="http://www.opengis.net/ows/1.1">ADORE DORIS interferometric processor</Title>
	  </Process>
	  <Status creationTime="2016-09-16T10:05:40.641+02:00">
	    <ProcessSucceeded>Process successful</ProcessSucceeded>
	  </Status>
	  <DataInputs />
	  <OutputDefinitions />
	  <ProcessOutputs>
	    <Output>
	      <Identifier xmlns="http://www.opengis.net/ows/1.1">result_osd</Identifier>
	      <Title xmlns="http://www.opengis.net/ows/1.1">OpenSearch Description to the Results</Title>
	      <Data>
	        <ComplexData mimeType="application/xml">
	          <Reference href="https://geohazards-tep.eo.esa.int/t2api/proxy?url=http%3a%2f%2fsb-10-16-10-20.dev.terradue.int%2fsbws%2fwps%2fdcs-doris-ifg%2f0000000-160901000010154-oozie-oozi-W%2fresults%2fdescription" mimeType="application/opensearchdescription+xml" />
	        </ComplexData>
	      </Data>
	    </Output>
	    <Output>
	      <Identifier xmlns="http://www.opengis.net/ows/1.1">result_distribution</Identifier>
	      <Title xmlns="http://www.opengis.net/ows/1.1">Result Files Distribution Package</Title>
	      <Data>
	        <ComplexData mimeType="application/xml">
	          <Reference href="http://sb-10-16-10-20.dev.terradue.int:50070/webhdfs/v1/ciop/run/dcs-doris-ifg/0000000-160901000010154-oozie-oozi-W/results.metalink?op=OPEN" mimeType="application/metalink4+xml" />
	        </ComplexData>
	      </Data>
	    </Output>
	  </ProcessOutputs>
	</ExecuteResponse>


Or failed


.. code-block:: xml

	<?xml version="1.0" encoding="us-ascii"?>
	<ExecuteResponse xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" service="WPS" version="1.0.0" xml:lang="en-GB" serviceInstance="https://geohazards-tep.eo.esa.int/t2api/wps/?Service=WPS&amp;Version=1.0.0&amp;Request=GetCapabilities" statusLocation="https://geohazards-tep.eo.esa.int/t2api/wps/RetrieveResultServlet?id=0c01sd28-0sc3-4f0f-8g7f-3df92eexcec3" xmlns="http://www.opengis.net/wps/1.0.0">
	  <Process d2p1:processVersion="1.0.0" xmlns:d2p1="http://www.opengis.net/wps/1.0.0">
	    <Identifier xmlns="http://www.opengis.net/ows/1.1">InSAR SBAS</Identifier>
	    <Title xmlns="http://www.opengis.net/ows/1.1">InSAR SBAS</Title>
	    <Abstract xmlns="http://www.opengis.net/ows/1.1">The InSAR Small BAseline Subsets (SBAS) algorithm has been developed by IREA-CNR for monitoring temporal evolution of surface deformations and to generate interferograms stacks as well. The InSAR Parallel-SBAS (P-SBAS) algorithm version has been integrated on the ESA's Grid Processing On Demand (G-POD) to exploit the avaialble High Performance Computing resources.</Abstract>
	  </Process>
	  <Status creationTime="2016-08-05T09:57:37Z">
	    <ProcessFailed>
	      <ExceptionReport version="1.0.0" xml:lang="en-GB" xmlns="http://www.opengis.net/ows/1.1">
	        <Exception exceptionCode="NoApplicableCode">
	          <ExceptionText>No error details available. Check for more information on the web portal.</ExceptionText>
	        </Exception>
	      </ExceptionReport>
	    </ProcessFailed>
	  </Status>
	  <DataInputs />
	  <OutputDefinitions />
	  <ProcessOutputs />
	</ExecuteResponse>
