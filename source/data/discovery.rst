
Discovery
---------

Exploring indices in the catalogue
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Let’s have a simple look at the indices available

Simple json
'''''''''''

.. code-block:: console

  curl -H "X-T2-Api:ABcdEF" "https://data.terradue.com/catalogue"

and the response as simple json

.. code-block:: json

    {
      "indices" : [
        {
          "name" : "sentinel1",
          "description" : "Index containing the datasets of Sentinel-1 space mission funded by the European Union and carried out by the ESA within the Copernicus Programme."
        },
        {
          "name" : "landsat8",
          "description" : "Index containing the datasets of Landsat-8 American Earth observation satellite launched on February 11, 2013. It is the eighth satellite in the Landsat program"
        },
        {
          "name" : "mrossi",
          "description" : "Personal User index containing datasets saved and published by the user Marco Rossi."
        }
      ]
    }


OpenSearch
''''''''''

The indices can be queried using :ref:`opensearch-client` with :ref:`base syndication model <syndicationmetadatamodel>` and filtered so.

.. code-block:: console

  opensearch-client -a "ABcdEF" "https://data.terradue.com/catalogue/search" identifier

and the response as the identifier list

.. code-block:: console

  sentinel1
  landsat8
  mrossi


Exploring series in the indices
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Indices can define subset of the entries they contain called :ref:`series`. The series can be discovered this way using curl.

.. code-block:: console

    curl "https://data.terradue.com/catalogue/mrossi/eop/series/search"

This command will return an atom feed with all the series in the indices mrossi


The same command with opensearch client and a few more parameter allows to find the link to search then in the series themselves

.. code-block:: console

    opensearch-client "https://data.terradue.com/catalogue/mrossi/eop/series/search" title,describes


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






