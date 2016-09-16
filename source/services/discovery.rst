Discovery
~~~~~~~~~

WPS GetCapabilities
===================

The webserver offers a GetCapabilites service, presenting all Web Processing Services accessible by the current user.

.. code-block:: http

    GET /t2api/wps/WebProcessingService?service=wps&request=GetCapabilities

The webserver acts as a proxy for all Web Processing Services added by the Administrator of the Portal.
He gather all GetCapabilities of all WPS and returns this as a GetCapabilities response. The response is conform to the WPS standard defined by OGC (http://schemas.opengis.net/wps/1.0.0).

.. code-block:: xml

	<?xml version="1.0" encoding="us-ascii"?>
	<wps:Capabilities xmlns:ows="http://www.opengis.net/ows/1.1" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:wps="http://www.opengis.net/wps/1.0.0">
	  <ows:ServiceIdentification>
	    <ows:Title>Geohazard Tep WPS</ows:Title>
	    <ows:Abstract>Proxy WPS of the geohazard platform</ows:Abstract>
	    <ows:Keywords>
	      <ows:Keyword>WPS</ows:Keyword>
	      <ows:Keyword>geohazards</ows:Keyword>
	      <ows:Keyword>geospatial</ows:Keyword>
	      <ows:Keyword>geoprocessing</ows:Keyword>
	    </ows:Keywords>
	    <ows:ServiceType>WPS</ows:ServiceType>
	    <ows:ServiceTypeVersion>1.0.0</ows:ServiceTypeVersion>
	    <ows:Fees>None</ows:Fees>
	    <ows:AccessConstraints>NONE</ows:AccessConstraints>
	  </ows:ServiceIdentification>
	  <ows:ServiceProvider>
	    <ows:ProviderName>Geohazards Tep</ows:ProviderName>
	    <ows:ProviderSite xlink:href="https://geohazards-tep.eo.esa.int/" />
	  </ows:ServiceProvider>
	  <ows:OperationsMetadata>
	    <ows:Operation name="GetCapabilities">
	      <ows:DCP>
	        <ows:HTTP>
	          <ows:Get xlink:href="https://geohazards-tep.eo.esa.int/t2api/wps/WebProcessingService" />
	        </ows:HTTP>
	      </ows:DCP>
	    </ows:Operation>
	    <ows:Operation name="DescribeProcess">
	      <ows:DCP>
	        <ows:HTTP>
	          <ows:Get xlink:href="https://geohazards-tep.eo.esa.int/t2api/wps/WebProcessingService" />
	        </ows:HTTP>
	      </ows:DCP>
	    </ows:Operation>
	    <ows:Operation name="Execute">
	      <ows:DCP>
	        <ows:HTTP>
	          <ows:Get xlink:href="https://geohazards-tep.eo.esa.int/t2api/wps/WebProcessingService" />
	          <ows:Post xlink:href="https://geohazards-tep.eo.esa.int/t2api/wps/WebProcessingService" />
	        </ows:HTTP>
	      </ows:DCP>
	    </ows:Operation>
	  </ows:OperationsMetadata>
	  <wps:ProcessOfferings>
	    <wps:Process wps:processVersion="1.0.0">
	      <ows:Identifier>9082cb5f-5066-4ccc-89f1-bd0f1aa19452</ows:Identifier>
	      <ows:Title>MERIS Mosaic COM</ows:Title>
	      <ows:Abstract>Service access point for the MERIS Mosaic COM G-POD service</ows:Abstract>
	    </wps:Process>
	    <wps:Process wps:processVersion="1.0.0">
	      <ows:Identifier>2a585ed3-8ch8-4717-aae8-a74af168907f</ows:Identifier>
	      <ows:Title>MIRAVI Geo</ows:Title>
	      <ows:Abstract>Service access point for the MIRAVI service. The request must specify the date and spatial range together with the dataset name</ows:Abstract>
	    </wps:Process>
	    <wps:Process wps:processVersion="1.0.0">
	      <ows:Identifier>c3a034c8-6b1r-4b5a-bf80-1b76f9920cae</ows:Identifier>
	      <ows:Title>BEAMARITHM</ows:Title>
	      <ows:Abstract>Service access point for the BEAMARITHM service</ows:Abstract>
	    </wps:Process>
	    <wps:Process wps:processVersion="1.0.0">
	      <ows:Identifier>2ceb1e69-6ab2-4ddb-9f7e-4a594924267c</ows:Identifier>
	      <ows:Title>ASAR PF</ows:Title>
	      <ows:Abstract>The ENVISAT ASAR PF is the ESA operational Level-1 processor developed by MDA. This processor, integrated on the ESA's Grid Processing On Demand , perform on-demand production of L1 products.</ows:Abstract>
	    </wps:Process>
	    <wps:Process wps:processVersion="1.0.0">
	      <ows:Identifier>59ae868d-d8ff-4e50-8ce7-5a213469820a</ows:Identifier>
	      <ows:Title>GAMMA Level-0</ows:Title>
	      <ows:Abstract>The GAMMA SAR and Interferometry Software is a collection of programs, developed by GAMMA Remote Sensing, which allows processing of SAR, interferometric SAR (InSAR) and differential interferometric SAR (DInSAR) data. The GAMMA Level-0 service, integrated on the ESA's Grid Processing On Demand (G-POD), performs the image focusing of ENVISAT ASAR Level-0 products.</ows:Abstract>
	    </wps:Process>
	    <wps:Process wps:processVersion="1.0.0">
		  <ows:Identifier>e748c24b-fr3e-48cb-a4a4-904d30fadc20</ows:Identifier>
		  <ows:Title>ADORE DORIS interferometric processor</ows:Title>
		  <ows:Abstract>ADORE DORIS interferometric processor</ows:Abstract>
		</wps:Process>
	  </wps:ProcessOfferings>
	  <wps:Languages>
	    <wps:Default>
	      <ows:Language>en-US</ows:Language>
	    </wps:Default>
	  </wps:Languages>
	</wps:Capabilities>

