
Discovery
---------

Exploring indices in the catalogue
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Let’s have a simple look at the indices available

Simple json
'''''''''''

.. code-block:: console

  curl -u mrossi:ABcdEF "https://catalog.terradue.com"

and the response as simple json

.. code-block:: json

    {
      "indices": [
          {
              "authors": [
                  {
                      "name": "Mario Rossi",
                      "mail": "mrossi@test.com"
                  }
              ],
              "created": "2016-06-03T10:30:42.7708920Z",
              "description": "Index containing the entries of the datasets published and saved by Mario Rossi.",
              "indexName": "mrossi",
              "lastMigrated": "2016-06-03T10:30:42.6951710Z",
              "version": 2
          },
          {
              "authors": [
                  {
                      "name": "Terradue DevOps team",
                      "uri": "https://www.terradue.com"
                  }
              ],
              "created": "2016-06-03T10:30:42.7708920Z",
              "description": "Index containing the entries of the datasets of Landsat-8 American Earth observation satellite launched on February 11, 2013. It is the eighth satellite in the Landsat program.",
              "indexName": "landsat8",
              "lastMigrated": "2016-06-03T10:30:42.6951710Z",
              "version": 2
          },
          {
              "authors": [
                  {
                      "name": "Terradue DevOps team",
                      "uri": "https://www.terradue.com"
                  }
              ],
              "created": "2016-06-03T10:30:42.7708920Z",
              "description": "Index containing the entries of the datasets of Envisat. Envisat was launched as an Earth observation satellite. Its objective was to service the continuity of European Remote-Sensing (ERS) Satellite missions, providing additional observational parameters to improve environmental studies.",
              "indexName": "envisat",
              "lastMigrated": "2016-06-03T10:30:42.6951710Z",
              "version": 2
          },
          {
              "authors": [
                  {
                      "name": "Terradue DevOps team",
                      "uri": "https://www.terradue.com"
                  }
              ],
              "created": "2016-06-03T10:30:42.7708920Z",
              "description": "Index containing the entries of the datasets of Sentinel-1 space mission funded by the European Union and carried out by the ESA within the Copernicus Programme.",
              "indexName": "sentinel1",
              "lastMigrated": "2016-06-03T10:30:42.6951710Z",
              "version": 2
          },
          {
              "authors": [
                  {
                      "name": "Terradue DevOps team",
                      "uri": "https://www.terradue.com"
                  }
              ],
              "created": "2016-06-03T10:30:42.7708920Z",
              "description": "Index containing the entries of the datasets of Sentinel-2. Sentinel-2 is an Earth observation mission developed by ESA as part of the Copernicus Programme to perform terrestrial observations in support of services such as forest monitoring, land cover changes detection, and natural disaster management.",
              "indexName": "sentinel2",
              "lastMigrated": "2016-06-03T10:30:42.6951710Z",
              "version": 2
          }
      ]
  }


OpenSearch
''''''''''

The indices can be queried using :ref:`opensearch-client` with :ref:`base syndication model <syndicationmetadatamodel>` and filtered so.

.. code-block:: console

  opensearch-client -u mrossi:ABcdEF "https://catalog.terradue.com/search" identifier

and the response as the identifier list

.. code-block:: console

  sentinel1
  landsat8
  mrossi


Exploring series in the indices
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Indices can define subset of the entries they contain called :ref:`series`. The series can be discovered this way using curl.

.. code-block:: console

    curl "https://catalog.terradue.com/mrossi/series/search"

This command will return an atom feed with all the series in the indices mrossi


The same command with opensearch client and a few more parameter allows to find the link to search then in the series themselves

.. code-block:: console

    opensearch-client "https://catalog.terradue.com/mrossi/series/search" title,describes


Exploring data packages in the portal
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

You also can discover all the :ref:`data packages <datapackage>` available from the portal.

.. code-block:: console

    curl "<portal_api_url>/data/package/search?q=etna"


This command will return an atom feed with all the data packages where there is mentionned "etna" in the title, keywords, tags or content.


The same command with opensearch client and a few more parameter allows to find the link to search then in the data packages themselves

.. code-block:: console

    opensearch-client "<portal_api_url>/data/package/search?q=etna" title,describes


This returns for instance

.. code-block:: console

    Etna November 2014,<portal_api_url>/data/package/etnanov2014/search


Then you can :ref:`search <search>` in the found data packageusing the url returned






