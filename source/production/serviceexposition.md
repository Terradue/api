# Explosition

## Search amongst results of a processing job

The webserver can be used as a proxy to query the list of results files of a processing job. For that, the webserver will read the Execute response associated to the job (accessible through the status location url of the wps service) and create from this an opensearch response.
To be compliant, the Execute response should be amongst one of the following cases:

### result osd

The response should contains one Output with Identifier = **result_osd** and a Reference pointing to an opensearch description url, which describe search query to get the
results files of the processing service as an atom feed. This solution is used on the Developer Cloud Sandboxes provided by Terradue.

```xml <?xml version="1.0" encoding="us-ascii"?> <wps:Output>         <ows:Identifier xmlns:ns1="http://www.opengis.net/ows/1.1">result_osd</ows:Identifier>         <ows:Title xmlns:ns1="http://www.opengis.net/ows/1.1">OpenSearch Description to the Results</ows:Title>                 <wps:Reference href="https://tep-geohazards-dev.terradue.com/t2api/proxy?url=http%3a%2f%2fsb-10-16-10-20.dev.terradue.int%2fsbws%2fwps%2fdcs-doris-ifg%2f0000023-160501000006641-oozie-oozi-W%2fresults%2fdescription" mimeType="application/opensearchdescription+xml" /> </wps:Output>

```

or (we accept also the Reference as ComplexData)

```xml
<?xml version="1.0" encoding="us-ascii"?>
<wps:Output>
        <ows:Identifier xmlns:ns1="http://www.opengis.net/ows/1.1">result_osd</ows:Identifier>
        <ows:Title xmlns:ns1="http://www.opengis.net/ows/1.1">OpenSearch Description to the Results</ows:Title>
        <wps:Data>
                <wps:ComplexData mimeType="application/xml">
                        <wps:Reference href="https://tep-geohazards-dev.terradue.com/t2api/proxy?url=http%3a%2f%2fsb-10-16-10-20.dev.terradue.int%2fsbws%2fwps%2fdcs-doris-ifg%2f0000023-160501000006641-oozie-oozi-W%2fresults%2fdescription" mimeType="application/opensearchdescription+xml" />
                </wps:ComplexData>
        </wps:Data>
</wps:Output>
```

### result metadata

The response should contains one Output with Identifier = **result_metadata** and a Reference pointing to a metadata file generated by the processing service and describing the results files as an atom feed.

```xml
<?xml version="1.0" encoding="us-ascii"?>
<wps:Output>
        <ows:Identifier xmlns:ns1="http://www.opengis.net/ows/1.1">result_metadata</ows:Identifier>
        <ows:Title xmlns:ns1="http://www.opengis.net/ows/1.1">OpenSearch Description to the Results</ows:Title>
                <wps:Reference href="http://sb-10-15-36-17.hydro.terradue.int/wpsoutputs/metadata.xml" method="GET" mimeType="application/atom+xml" />
</wps:Output>
```

or (we accept also the Reference as ComplexData)

```xml
<?xml version="1.0" encoding="us-ascii"?>
<wps:Output>
        <ows:Identifier xmlns:ns1="http://www.opengis.net/ows/1.1">result_metadata</ows:Identifier>
        <ows:Title xmlns:ns1="http://www.opengis.net/ows/1.1">OpenSearch Description to the Results</ows:Title>
        <wps:Data>
                <wps:ComplexData mimeType="application/xml">
                        <wps:Reference href="http://sb-10-15-36-17.hydro.terradue.int/wpsoutputs/metadata.xml" method="GET" mimeType="application/atom+xml" />
                </wps:ComplexData>
        </wps:Data>
</wps:Output>
```

example of metadata.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<feed xmlns="http://www.w3.org/2005/Atom">
  <title type="text">Discovery feed for WPS result local data</title>
  <subtitle type="text">This OpenSearch Service allows the discovery of the different items which are part of the localdata collection. This search service is in accordance with the OGC 10-032r3 specification.</subtitle>
  <generator>Terradue Web Server</generator>
  <entry>
    <id>AATSR_output.png</id>
    <title type="text">AATSR_output.png</title>
    <published>2016-06-15T10:27:30.711606Z</published>
    <updated>2016-06-15T10:27:30.711606Z</updated>
    <link href="http://sb-10-15-36-17.hydro.terradue.int/wpsoutputs/AATSR_output.png?op=OPEN" rel="enclosure" type="application/octet-stream"/>
    <identifier xmlns="http://purl.org/dc/elements/1.1/">AATSR_output.png</identifier>
    <where xmlns="http://www.georss.org/georss/10" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
      <Polygon xmlns="http://www.opengis.net/gml">
        <exterior>
          <LinearRing>
            <posList srsDimension="2">30.5009918 0.9953687 30.5009918 -4.2681770 35.9339877 -4.2681770 35.9339877 0.9953687 30.5009918 0.9953687</posList>
          </LinearRing>
        </exterior>
      </Polygon>
    </where>
    <box xmlns="http://www.georss.org/georss">30.5009918 -4.2681770 35.9339877 0.9953687</box>
    <offering xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://www.opengis.net/owc/1.0" code="http://www.opengis.net/spec/owc-atom/1.0/req/png">
      <content href="http://sb-10-15-36-17.hydro.terradue.int/wpsoutputs/AATSR_output.png?op=OPEN" type="image/png" />
    </offering>
  </entry>
  <entry>
        <id>http://sb-10-15-36-17/HEP_tests/qgis_outputs/AATSR_output.tif</id>
    <title type="text">AATSR_output.tif</title>
        <published>2016-06-15T10:27:30.711606Z</published>
    <updated>2016-06-15T10:27:30.711606Z</updated>
    <link href="http://sb-10-15-36-17.hydro.terradue.int/wpsoutputs/AATSR_output.tif?op=OPEN" rel="enclosure" type="application/octet-stream"/>
    <identifier xmlns="http://purl.org/dc/elements/1.1/">AATSR_output.tif</identifier>
    <where xmlns="http://www.georss.org/georss/10" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
      <Polygon xmlns="http://www.opengis.net/gml">
        <exterior>
          <LinearRing>
            <posList srsDimension="2">30.5009918 0.9953687 30.5009918 -4.2681770 35.9339877 -4.2681770 35.9339877 0.9953687 30.5009918 0.9953687</posList>
          </LinearRing>
        </exterior>
      </Polygon>
    </where>
    <box xmlns="http://www.georss.org/georss">30.5009918 -4.2681770 35.9339877 0.9953687</box>
    <offering xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://www.opengis.net/owc/1.0" code="http://www.opengis.net/spec/owc-atom/1.0/req/png">
      <content href="http://sb-10-15-36-17.hydro.terradue.int/wpsoutputs/AATSR_output.tif?op=OPEN" type="image/tif" />
      </offering>
  </entry>
  <identifier xmlns="http://purl.org/dc/elements/1.1/">localdata</identifier>
  <queryTime xmlns="http://purl.org/dc/elements/1.1/">0.0002</queryTime>
  <startIndex xmlns="http://a9.com/-/spec/opensearch/1.1/">1</startIndex>
  <itemsPerPage xmlns="http://a9.com/-/spec/opensearch/1.1/">50</itemsPerPage>
  <os:Query os:count="50" os:language="" os:searchTerms="" os:startIndex="" os:startPage="" xmlns:os="http://a9.com/-/spec/opensearch/1.1/" xmlns:param="http://a9.com/-/spec/opensearch/extensions/parameters/1.0/"/>
</feed>
```

### result metalink (list of files)

The response should contains one Output with a **metalink** element, containing a list of files, pointing to the results files processed by the service.

```xml
<?xml version="1.0" encoding="us-ascii"?>
<wps:Output>
        <ows:Identifier>ResultDescription</ows:Identifier>
        <ows:Title>List of output files produced by the process</ows:Title>
        <wps:Data>
                <wps:ComplexData>
                        <metalink xmlns="http://www.metalinker.org" xmlns:owl="http://www.w3.org/2002/07/owl#" xmlns:ws="http://dclite4g.xmlns.com/ws.rdf#" version="3.0" type="dynamic">
                                <files>
                                        <file name="http://gpod.eo.esa.int/5833f9b6-721f-47db-8b6c-c9e4278b24a9/1">
                                                <releasedate>2016-05-12T08:56:21Z</releasedate>
                                                <identity>http://gpod.eo.esa.int/5833f9b6-721f-47db-8b6c-c9e4278b24a9/1</identity>
                                                <resources>
                                                        <url type="http">http://gpod.eo.esa.int/results/5833f9b6-721f-47db-8b6c-c9e4278b24a9/ASA_IM__0CNPAM20050615_204642_000000152038_00129_17217_2705.autof</url>
                                                </resources>
                                        </file>
                                        <file name="http://gpod.eo.esa.int/5833f9b6-721f-47db-8b6c-c9e4278b24a9/2">
                                                <releasedate>2016-05-12T08:56:21Z</releasedate>
                                                <identity>http://gpod.eo.esa.int/5833f9b6-721f-47db-8b6c-c9e4278b24a9/2</identity>
                                                <resources>
                                                        <url type="http">http://gpod.eo.esa.int/results/5833f9b6-721f-47db-8b6c-c9e4278b24a9/ASA_IM__0CNPAM20050615_204642_000000152038_00129_17217_2705.azsp</url>
                                                </resources>
                                        </file>
                                </files>
                        </metalink>
                </wps:ComplexData>
        </wps:Data>
</wps:Output>
```

### result metalink (atom entry)

The response should contains one Output with a **metalink** element, containing at least list one file with the .atom extension, pointing to a metadata file generated by the processing service and describing the results files as an atom feed. This atom feed is used as search response by the geobrowser widget displaying the results.

```xml
<?xml version="1.0" encoding="us-ascii"?>
<wps:Output>
        <ows:Identifier>ResultDescription</ows:Identifier>
        <ows:Title>List of output files produced by the process</ows:Title>
        <wps:Data>
                <wps:ComplexData>
                        <metalink xmlns="http://www.metalinker.org" xmlns:owl="http://www.w3.org/2002/07/owl#" xmlns:ws="http://dclite4g.xmlns.com/ws.rdf#" version="3.0" type="dynamic">
                                <files>
                                        <file name="http://gpod.eo.esa.int/5833f9b6-721f-47db-8b6c-c9e4278b24a9/1">
                                                <releasedate>2016-05-12T08:56:21Z</releasedate>
                                                <identity>http://gpod.eo.esa.int/5833f9b6-721f-47db-8b6c-c9e4278b24a9/1</identity>
                                                <resources>
                                                        <url type="http">http://gpod.eo.esa.int/results/5833f9b6-721f-47db-8b6c-c9e4278b24a9/ASA_IM__0CNPAM20050615_204642_000000152038_00129_17217_2705.atom</url>
                                                </resources>
                                        </file>
                                </files>
                        </metalink>
                </wps:ComplexData>
        </wps:Data>
</wps:Output>
```

## Visualize results of a processing job

To be visualized into the geobrowser, a job processing should expose an opensearch description in the Execute response of the status location url.
The Execute response can directly have a description link associated (see [result osd]). Otherwise, the webserver will be used as a proxy to enable an opensearch request over the results (see [Search amongst results of a processing job]).

### Quicklook visualisation

For the entry to be visualized as quicklook on the geobrowser, the search result should contain one entry with an **offering** element (see [http://www.opengis.net/owc/1.0](http://www.opengis.net/owc/1.0)) - which can be a png or a geotiff, used then as quicklook - as well as a **box** element (see [http://www.georss.org/georss](http://www.georss.org/georss)) to be able to know where to put it on the map.

```xml
<owc:offering xmlns:owc="http://www.opengis.net/owc/1.0" code="http://www.opengis.net/spec/owc-atom/1.0/req/geotiff">
        <owc:content href="https://store.terradue.com//api//production/workflows/flood-map-extent/runs/0000029-161103111819075-oozie-oozi-W/20150404_VV_water_mask.tif" type="image/tiff" />
</owc:offering>
<owc:offering xmlns:owc="http://www.opengis.net/owc/1.0" code="http://www.opengis.net/spec/owc-atom/1.0/req/img">
        <owc:content href="https://store.terradue.com//api//production/workflows/flood-map-extent/runs/0000029-161103111819075-oozie-oozi-W/20150404_VV_water_mask.png" type="image/png" />
</owc:offering>
```

### Metadata visualisation

Metadata associated to the entry will be displayed in a popup on the geobrowser when user clicks on the entry. The value is taken directly as html from the **summary** element.

```xml
<summary type="html">
        <table> <tbody> <tr> <td><table valign="top"> <tbody> <tr> <td><strong>Identifier</strong></td><td>0000029-161103111819075-oozie-oozi-W/20150404_VV_water_mask.tif</td> </tr> </tbody> </table></td> </tr><tr> <td></td> </tr> </tbody> </table>
</summary>
```

### Files download

The list of downlodable files is taken from the list of **link** elements with rel = "enclosure". The **title** element is used as title on the download list.

```xml
<link rel="enclosure" type="application/octet-stream" title="tif file via Data Gateway" length="9282529" href="https://store.terradue.com///production/workflows/flood-map-extent/runs/0000029-161103111819075-oozie-oozi-W/20150404_VV_water_mask.tif" />
<link rel="enclosure" type="application/octet-stream" title="png file via Data Gateway" length="43457" href="https://store.terradue.com///production/workflows/flood-map-extent/runs/0000029-161103111819075-oozie-oozi-W/20150404_VV_water_mask.png" />
<link rel="enclosure" type="application/octet-stream" title="pngw file via Data Gateway" length="150" href="https://store.terradue.com///production/workflows/flood-map-extent/runs/0000029-161103111819075-oozie-oozi-W/20150404_VV_water_mask.pngw" />
```

## World files and properties

When using the Cloud Sandbox provided by Terradue, the service performing the search over the results is able to read world file (**\<filename>.pngw**) presents in the result folder and generate the box and the geometry (using gdal) associated to the png.

It also possible to add in the result folder a java properties file (key=value), named **\<filename>.properties**, to give additional information about an output file of the proecess. This additional information will be added into the atom entry of the output file as metadata information.
All keywords / value from the .properties file are added as a table to the \<summary> element (used for metadata display on the geobrowser).
Some keywords however, perform an update on the OWS context result:

> - **identifier** (set the identifier value)
> - **date** (startDate/endDate - set StartDate and EndDate values)
> - **title** (set the title)
> - **geometry** (set the spatial element as well as the box element. If present, this value is prioritary over the one generated by Gdal. Must be WKT format)
> - **image_url** (<http:/>/\<my_image_url> or <file:/>/\<my_image_path> - add an image in the summary table)