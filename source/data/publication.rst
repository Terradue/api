
Publication
-----------

In this part, we will discover how to publish our own entries in the catalogue.

Personal index management
^^^^^^^^^^^^^^^^^^^^^^^^^

Every user of the platform has its own index called with the username (e.g user Mario Rossi [username: mrossi] has an index called mrossi).

This index should be created automatically when the user is registered on the T2 Cloud Platform. You can check the existence of your own index by querying the description deocument of it.

.. code-block:: console

  curl -u mrossi:ABcdEF "https://catalogue.terradue.com/mrossi/description"


.. note:: replace **mrossi** by your own username

If by any chance, you index does not exist yet, you can simply create it by yourself with the following command.

.. code-block:: console

  curl -XPUT -u mrossi:ABcdEF "https://catalogue.terradue.com/mrossi"


A successful command should return

.. code-block:: json

    {
      "name": "mrossi_v1",
      "shards": {
          "total": 10,
          "successful": 10,
          "failed": 0
      },
      "types": [
          {
              "name": "series",
              "version": 2,
              "description": "Type representing a series"
          },
          {
              "name": "gtfeature",
              "version": 2,
              "description": "Type representing a feature geo and timed"
          },
          {
              "name": "eopfeature",
              "version": 2,
              "description": "Type representing an Earth Observation feature"
          },
          {
              "name": "eopseries",
              "version": 2,
              "description": "Type representing a EarthObservation series"
          },
          {
              "name": "eoporbit",
              "version": 1,
              "description": "Type representing an orbit information"
          },
          {
              "name": "eoppoint",
              "version": 2,
              "description": "Type representing an orbit information"
          }
      ]
  }

Index Metadata update
"""""""""""""""""""""

.. note:: coming soon


Now your index ready, you can start publishing entries in the catalogue. The following section describes how to create, update or delete entries in your index.

.. _datacreateentries :

Create entries
^^^^^^^^^^^^^^

As described in the :ref:`Metadata model section <syndicationmetadatamodel>`, one or more entries are represented in a feed and this is this feed you will post to the catalogue to be indexed. The supported formats of this feed are listed in the :ref:`mediatype` section but here we will always use `Atom <https://tools.ietf.org/html/rfc4287>`_.

Let's insert our first entry. We then write a file on your local file system (e.g. myfirstfeed.atom) with our first feed:

.. code-block:: xml

    <feed xmlns="http://www.w3.org/2005/Atom">
      <title type="text">My first feed</title>
      <id>test</id>
      <entry>
        <id>entry1</id>
        <identifier xmlns="http://purl.org/dc/elements/1.1/">S2A_OPER_MSI_L1C_TL_SGS__20160625T170310_A005267_T32TQM_N02.04</identifier>
        <title type="text">Imager - Sentinel2 - 2016-06-25T10:06:17</title>
        <summary type="html">
          &lt;table&gt;
            &lt;tr&gt;&lt;td&gt;&lt;strong&gt;Mission&lt;/strong&gt;&lt;/td&gt;&lt;td&gt;Sentinel-2&lt;/td&gt;&lt;/tr&gt;
            &lt;tr&gt;&lt;td&gt;&lt;strong&gt;Orbit&lt;/strong&gt;&lt;/td&gt;&lt;td&gt;005267 DESCENDING&lt;/td&gt;&lt;/tr&gt;
            &lt;tr&gt;&lt;td&gt;&lt;strong&gt;Track&lt;/strong&gt;&lt;/td&gt;&lt;td&gt;122&lt;/td&gt;&lt;/tr&gt;
            &lt;tr&gt;&lt;td&gt;&lt;strong&gt;Cloud Cover&lt;/strong&gt;&lt;/td&gt;&lt;td&gt;0.1674&lt;/td&gt;&lt;/tr&gt;
            &lt;tr&gt;&lt;td&gt;&lt;strong&gt;Date&lt;/strong&gt;&lt;/td&gt;&lt;td&gt;2016-06-25T10:06:17.4130000Z&lt;/td&gt;&lt;/tr&gt;
          &lt;/table&gt;
        </summary>
        <date xmlns="http://purl.org/dc/elements/1.1/">2016-06-25T10:06:17.4130000Z</date>
        <spatial xmlns="http://purl.org/dc/terms/">POLYGON((11.430710453849 42.4269119937756,12.7055623149861 42.4269119937756,12.7055623149861 41.4040347436697,11.430710453849 41.4040347436697,11.430710453849 42.4269119937756))</spatial>  
        <published>2014-12-05T20:58:38.024Z</published>
        <link rel="enclosure" type="application/octet-stream" length="4195720" href="https://store.terradue.com/" />
      </entry>
    </feed>

This is a single entry feed for training purpose but it could contains many more. Let's explain it element by element.


* **feed** *mandatory* : this is the main container
* **feed/title** *optional* : this is the title of the feed and is there only for educational purpose but is useless for the catalogue
* **feed/id** *optional* : this is the identifier of the feed and is there only for educational purpose but is useless for the catalogue
* **feed/entry** *mandatory* : this is the container for an entry in the catalogue
* **feed/entry/id** *optional* : this is the identifier of the entry and is there only for educational purpose but is useless for the catalogue
* **feed/identifier** *mandatory* : this is the unique identifier of the entry. This is a **very important** element since it will define the unique identifier of the entry in the index. Any other element with the same identifier in the same index will be overriden.
* **feed/entry/title** *mandatory* : this is the title of the entry and is usually used by other component (e.g. portal) to display the item caption (e.g. in the list of results).
* **feed/entry/summary** *optional* : this is the short description (abstract) of the entry. It can be set as HTML (XML encoded) as in the example but can also be a simple text. In this latter case, the attribute ``type`` will be set to "text". Even if optional, this element is important because it is often used by the other component such as the portal to display a summary of the item. For instance, in the thematic applications of the portal, the summary is used to fill in the info bubble of the item displayed on the map.
* **feed/entry/date** *optional* : this is one of the element used in the :ref:`geotimemetadatamodel`. It defines the temporal charateristic of the entry. It may define a time instant (cf. example) or a time range. The format of the date(s) must follow ISO8601.
  
  .. code-block:: xml
  
      <!-- Time instant -->
      <date xmlns="http://purl.org/dc/elements/1.1/">2016-06-25T10:06:17.4130000Z</date>


  .. code-block:: xml
  
      <!-- Time range -->
      <date xmlns="http://purl.org/dc/elements/1.1/">2016-06-25T10:06:17.4130000Z/2016-06-25T10:36:17.4130000Z</date>


* **feed/entry/spatial** *optional* : this is the other element used in the :ref:`geotimemetadatamodel`. It defines the spatial charateristic of the entry. There are several way of defining the geometry of the entry:

  .. code-block:: xml
  
      <!-- Well-Known-Text -->
      <spatial xmlns="http://purl.org/dc/terms/">POLYGON((11.430710453849 42.4269119937756,12.7055623149861 42.4269119937756,12.7055623149861 41.4040347436697,11.430710453849 41.4040347436697,11.430710453849 42.4269119937756))</spatial>  

  .. code-block:: xml
  
      <!-- GeoRSS polygon -->
      <georss:polygon xmlns:georss="http://www.georss.org/georss">42.4269119937756 11.430710453849 42.4269119937756 12.7055623149861 41.4040347436697 12.7055623149861 41.4040347436697 11.430710453849 42.4269119937756 11.430710453849</georss:polygon>

  .. code-block:: xml
  
      <!-- GeoRSS where with GML -->
      <georss:where xmlns:georss="http://www.georss.org/georss">
        <gml:MultiSurface>
          <gml:surfaceMembers>
            <gml:Polygon>
              <gml:exterior>
                <gml:LinearRing>
                  <gml:posList count="5">
                  42.4269119937756 11.430710453849 42.4269119937756 12.7055623149861 41.4040347436697 12.7055623149861 41.4040347436697 11.430710453849 42.4269119937756 11.430710453849
                  </gml:posList>
                </gml:LinearRing>
              </gml:exterior>
            </gml:Polygon>
          </gml:surfaceMembers>
        </gml:MultiSurface>
      </georss:polygon>

* **feed/entry/published** *optional* : this is the element defining the publication date of the entry in the index. If not specified, it will be set at the time the entry is indexed in the catalogue. The format of the date must follow ISO8601.
* **feed/entry/link** *optional* : several links may be associated to an entry in the catalogue. They are important references for other components of the platform. The link is set in ``href`` sttribute. The resulting content of the link is defined by the ``type`` attribute and the purpose of the link is defined by the ``rel`` attribute:

+-----------+---------------------------------------------------------------------------------------------+
| rel       | purpose                                                                                     |
+===========+=============================================================================================+
| enclosure | Identifies a related resource that is potentially large and might require special handling. |
|           | Usually used for the dataset download that the entry is describing. Many enclosures may be  |
|           | defined to specify many download point                                                      |
+-----------+---------------------------------------------------------------------------------------------+
| alternate | Refers to a substitute for this entry.                                                      |
+-----------+---------------------------------------------------------------------------------------------+


Now we have our file we can send it to the catalogue for indexing.

.. code-block:: console

  curl -u mrossi:ABcdEF -XPOST -H "Content-Type: application/atom+xml" -d@myfirstfeed.atom "https://catalog.terradue.com/mrossi"


.. note:: Please note the ``Content-Type`` header set to ``application/atom+xml``. This is important to indicate the catalogue the :ref:`mediatype` of the feed posted.

The resulting response from the catalogue is a json reporting the actions done in the index

.. code-block:: json

    {
      "added": 1,
      "updated": 0,
      "deleted": 0,
      "errors": 0,
      "items": [
          {
              "id": "S2A_OPER_MSI_L1C_TL_SGS__20160625T170310_A005267_T32TQM_N02.04",
              "type": "gtfeature",
              "operation": "Add"
          }
      ]
    }


You have now a new entry in your index. You can check it has been indexed correctly by making some queries

This command returns the same feed you just sent (with some more information of the catalogue):

.. code-block:: console

    curl -u mrossi:ABcdEF "https://catalog.terradue.com/mrossi/search?uid=S2A_OPER_MSI_L1C_TL_SGS__20160625T170310_A005267_T32TQM_N02.04"


This command using opensearch-client makes a temporal and spatial search and return the download link correctly

.. code-block:: console

    opensearch-client -u mrossi:ABcdEF -p bbox=10,40,12,42 -p start=2016-06-24 -p stop=2016-06-26 "https://catalog.terradue.com/mrossi/search" enclosure


.. note:: The above example showed the insertion of one entry at a time but remember that you can send as many entries in the same feed as you want. There is only a limit of 32Mbytes maximum by feed sent.


Update entries
^^^^^^^^^^^^^^

The update of updating entries in the index is the same as per creation. If you specify the same identifier element, the corresponding entry will be simply updated. The catalogue shall return a response similar to this one:

.. code-block:: json

    {
      "added": 0,
      "updated": 1,
      "deleted": 0,
      "errors": 0,
      "items": [
          {
              "id": "S2A_OPER_MSI_L1C_TL_SGS__20160625T170310_A005267_T32TQM_N02.04",
              "type": "gtfeature",
              "operation": "Update"
          }
      ]
    }


Delete entries
^^^^^^^^^^^^^^

Deleting one or more entries is done as per searching for them.

To delete a single entry by reference:

.. code-block:: console

    curl -u mrossi:ABcdEF -X DELETE "https://catalog.terradue.com/mrossi/query?uid=S2A_OPER_MSI_L1C_TL_SGS__20160625T170310_A005267_T32TQM_N02.04


and it returns :

.. code-block:: json

    {
      "added": 0,
      "updated": 0,
      "deleted": 1,
      "errors": 0,
      "items": [
          {
              "id": "S2A_OPER_MSI_L1C_TL_SGS__20160625T170310_A005267_T32TQM_N02.04",
              "type": "gtfeature",
              "operation": "Delete"
          }
      ]
    }


To delete many entries by query (e.g. all data of 2012):

.. code-block:: console

    curl -u mrossi:ABcdEF -X DELETE "https://catalog.terradue.com/mrossi/query?start=2012-01-01&stop=2012-12-31



.. note:: please note that the action part of the url is ``query`` and not ``search``. It's on purpose to avoid wrong manipulation between searching and deleting.



Create Series
^^^^^^^^^^^^^

It is also possible to create set of index entries based on common fixed parameters. In order to create one this set called :ref:`series`, we will also index to the catalogue a feed with one or more entries that will define one or more series. Let's start with the file seriesitaly.atom

.. code-block:: xml

    <feed xmlns="http://www.w3.org/2005/Atom">
      <title type="text">My second feed</title>
      <id>test</id>
      <entry>
        <id>series1</id>
        <title type="text">Data over Italy</title>
        <published>2016-06-03T10:30:45.879747Z</published>
        <link rel="describedBy" type="application/atom+xml" title="search filters for Italy AOI" href="https://catalog.terradue.com/mrossi/search?geom=POLYGON((6.372 47.01,19.028 47.01,18.896 36.527,6.46 36.598,6.372 47.01))" />
        <identifier xmlns="http://purl.org/dc/elements/1.1/">italy</identifier>
      </entry>
    </feed>

The description of the elements done in the :ref:`datacreateentries` section are still valid. Here are the specific elements of a series.

* **feed/identifier** *mandatory* : this is the unique identifier of the series. This is a **very important** element since it will define the unique identifier of the series in the index and the route (URL) to access the series. Any other series with the same identifier in the same index will be overriden.
* **feed/entry/link[rel='describedBy']** *mandatory* : Those links are specific to series, it defines one or more set that constitutes the series. In the example the link is
  
.. code-block:: console

    https://catalog.terradue.com/mrossi/search?geom=POLYGON((6.372 47.01,19.028 47.01,18.896 36.527,6.46 36.598,6.372 47.01))


this link is a spatial filter request. All index entries returned by this query will be part of the series.

Now, let's post the series in the catalogue with the following command

.. code-block:: console

  curl -u mrossi:ABcdEF -XPOST -H "Content-Type: application/atom+xml" -d@seriesitaly.atom "https://catalog.terradue.com/mrossi/series"


and returns

.. code-block:: json

    {
        "added": 1,
        "updated": 0,
        "deleted": 0,
        "errors": 0,
        "items": [
            {
                "id": "italy",
                "type": "series",
                "operation": "Add"
            }
        ]
    }


The series is successfully created and we can query it 

.. code-block:: console

    opensearch-client https://catalog.terradue.com/mrossi/series/italy/search


Updating and deleting series is done using the same mechanism as per entries but inserting the /series after the index name.





