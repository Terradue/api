Description
~~~~~~~~~~~

WPS DescribeProcess
===================

The webserver offers a DescribeProcess service, describing a given WPS service.

.. code-block:: http

    GET t2api/wps/WebProcessingService?service=wps&request=DescribeProcess&version=<serviceVersion>&identifier=<service_identifier>

The webserver acts as a proxy for all Web Processing Services added by the Administrator of the Portal.
He gets the DescribeProcess offered by the WPS and returns it as a DescribeProcess response. The response is conform to the WPS standard defined by OGC (http://schemas.opengis.net/wps/1.0.0).

.. code-block:: xml

	<?xml version="1.0" encoding="us-ascii"?>
	<wps:ProcessDescriptions service="WPS" version="1.0.0" xml:lang="en-US" xmlns:wps="http://www.opengis.net/wps/1.0.0">
	  <ProcessDescription wps:processVersion="1.0.0" storeSupported="true" statusSupported="true">
	    <Identifier xmlns="http://www.opengis.net/ows/1.1">com.terradue.wps_oozie.process.OozieAbstractAlgorithm</Identifier>
	    <Title xmlns="http://www.opengis.net/ows/1.1">ADORE DORIS interferometric processor</Title>
	    <Abstract xmlns="http://www.opengis.net/ows/1.1">ADORE DORIS interferometric processor</Abstract>
	    <DataInputs>
	      <Input minOccurs="1" maxOccurs="100">
	        <Identifier xmlns="http://www.opengis.net/ows/1.1">slave</Identifier>
	        <Title xmlns="http://www.opengis.net/ows/1.1">Slave product reference</Title>
	        <Abstract xmlns="http://www.opengis.net/ows/1.1">Define the slave product reference to use with ADORE</Abstract>
	        <LiteralData>
	          <DataType d6p1:reference="xs:string" xmlns:d6p1="http://www.opengis.net/ows/1.1" xmlns="http://www.opengis.net/ows/1.1">string</DataType>
	          <AnyValue xmlns="http://www.opengis.net/ows/1.1" />
	          <DefaultValue>http://eo-virtual-archive4.esa.int/search/ASA_IMS_1P/ASA_IMS_1PNDPA20080326_204749_000000162067_00129_31746_3124.N1/rdf</DefaultValue>
	        </LiteralData>
	      </Input>
	      <Input minOccurs="1" maxOccurs="100">
	        <Identifier xmlns="http://www.opengis.net/ows/1.1">poi</Identifier>
	        <Title xmlns="http://www.opengis.net/ows/1.1">Point of interest</Title>
	        <Abstract xmlns="http://www.opengis.net/ows/1.1">Point of interest WKT, e.g. POINT(longitude latitude)</Abstract>
	        <LiteralData>
	          <DataType d6p1:reference="xs:string" xmlns:d6p1="http://www.opengis.net/ows/1.1" xmlns="http://www.opengis.net/ows/1.1">string</DataType>
	          <AnyValue xmlns="http://www.opengis.net/ows/1.1" />
	          <DefaultValue>POINT(13.4 42.35)</DefaultValue>
	        </LiteralData>
	      </Input>
	      <Input minOccurs="1" maxOccurs="100">
	        <Identifier xmlns="http://www.opengis.net/ows/1.1">extent</Identifier>
	        <Title xmlns="http://www.opengis.net/ows/1.1">Extent</Title>
	        <Abstract xmlns="http://www.opengis.net/ows/1.1">extent</Abstract>
	        <LiteralData>
	          <DataType d6p1:reference="xs:string" xmlns:d6p1="http://www.opengis.net/ows/1.1" xmlns="http://www.opengis.net/ows/1.1">string</DataType>
	          <AnyValue xmlns="http://www.opengis.net/ows/1.1" />
	          <DefaultValue>2000,2000</DefaultValue>
	        </LiteralData>
	      </Input>
	      <Input minOccurs="1" maxOccurs="100">
	        <Identifier xmlns="http://www.opengis.net/ows/1.1">settings</Identifier>
	        <Title xmlns="http://www.opengis.net/ows/1.1">Settings for ADORE Doris separated by comma</Title>
	        <Abstract xmlns="http://www.opengis.net/ows/1.1">Settings for ADORE Doris separated by comma</Abstract>
	        <LiteralData>
	          <DataType d6p1:reference="xs:string" xmlns:d6p1="http://www.opengis.net/ows/1.1" xmlns="http://www.opengis.net/ows/1.1">string</DataType>
	          <AnyValue xmlns="http://www.opengis.net/ows/1.1" />
	          <DefaultValue>cc_winsize="128 128",fc_acc="8 8",int_multilook="4 4",coh_multilook="4 4",dumpbaseline="15 10"</DefaultValue>
	        </LiteralData>
	      </Input>
	      <Input minOccurs="1" maxOccurs="100">
	        <Identifier xmlns="http://www.opengis.net/ows/1.1">master</Identifier>
	        <Title xmlns="http://www.opengis.net/ows/1.1">master product reference</Title>
	        <Abstract xmlns="http://www.opengis.net/ows/1.1">Define the master product reference to use with ADORE</Abstract>
	        <LiteralData>
	          <DataType d6p1:reference="xs:string" xmlns:d6p1="http://www.opengis.net/ows/1.1" xmlns="http://www.opengis.net/ows/1.1">string</DataType>
	          <AnyValue xmlns="http://www.opengis.net/ows/1.1" />
	          <DefaultValue>http://eo-virtual-archive4.esa.int/search/ASA_IMS_1P/ASA_IMS_1PNDPA20090311_204746_000000162077_00129_36756_3125.N1/rdf</DefaultValue>
	        </LiteralData>
	      </Input>
	    </DataInputs>
	    <ProcessOutputs>
	      <Output>
	        <Identifier xmlns="http://www.opengis.net/ows/1.1">result_distribution</Identifier>
	        <Title xmlns="http://www.opengis.net/ows/1.1">Result Files Distribution Package</Title>
	        <Abstract xmlns="http://www.opengis.net/ows/1.1">This process returns a file with the list of result products.
	The default is Metalink document that is an extensible metadata file format that describes one or more computer files available for download. It specifies files appropriate for the user's language and operating system; facilitates file verification and recovery from data corruption.</Abstract>
	        <ComplexOutput>
	          <Default>
	            <Format>
	              <MimeType>application/xml</MimeType>
	            </Format>
	          </Default>
	          <Supported>
	            <Format>
	              <MimeType>application/xml</MimeType>
	            </Format>
	          </Supported>
	        </ComplexOutput>
	      </Output>
	      <Output>
	        <Identifier xmlns="http://www.opengis.net/ows/1.1">result_osd</Identifier>
	        <Title xmlns="http://www.opengis.net/ows/1.1">OpenSearch Description to the Results</Title>
	        <ComplexOutput>
	          <Default>
	            <Format>
	              <MimeType>application/xml</MimeType>
	            </Format>
	          </Default>
	          <Supported>
	            <Format>
	              <MimeType>application/xml</MimeType>
	            </Format>
	          </Supported>
	        </ComplexOutput>
	      </Output>
	    </ProcessOutputs>
	  </ProcessDescription>
	</wps:ProcessDescriptions>

