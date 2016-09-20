.. _search:

Search
------

Now, we will see how to query different type of :ref:`collection` : :ref:`index`, :ref:`series` or :ref:`data package <datapackage>`

Auto description
^^^^^^^^^^^^^^^^

Every point of access for any type of collection must expose a description document. It is a self descriptive XML document that declares the entry points for the search and the parameters that can be searched.

Let's query the raw XML using curl

.. code-block:: console

    curl "https://catalog.terradue.com/mrossi/description"



Now, let's use opensearch-client to format it in a human readable way

.. code-block:: console

    opensearch-client -d "https://catalog.terradue.com/mrossi/description"


.. code-block:: console

    name       O/M description
    ----       --- -----------
    format       O content type of the query [*atom|json|atomeop|rdf]
    q            O generic search terms
    uid          O identifier of the entry within the collection
    update       O timestamp < publication date (creation or update) 
    bbox         O spatial coverage in form minX,minY,maxX,maxY
    geom         O spatial coverage in WKT form
    grel         O spatial relationship [*intersects|contains|disjoint]
    ...


.. warning:: Do not confuse query filters and properties keywords!

    Even if they may have a relationship, the name used for **query filters** do not always correspond exactly to the **properties keywords** extractor used in opensearch-client.
    For instance, when you filter on the identifier, you use the filter ``uid``, when you request the identifier, you use ``identifier``


Query with filters
^^^^^^^^^^^^^^^^^^

We will perform the query using parameters


With curl

.. code-block:: console

    curl "https://catalog.terradue.com/mrossi/search?format=atom&q=processing&bbox=60,-30,70,-20"


The same with opensearch-client

.. code-block:: console
  
    opensearch-client -f atom -p q=processing -p bbox=60,-30,70,-20 "https://catalog.terradue.com/mrossi/search?format=json&q=processing&bbox=60,-30,70,-20" {}


Both previous commands will return the atom feed with the result queried.


Query specific properties
^^^^^^^^^^^^^^^^^^^^^^^^^

With :ref:`opensearch-client`, it is possible to query some specific entry properties according to the metadata model of the resource. 


.. note:: See the :ref:`opensearch-client` doc section to know how to list all the metadata properties extractor available per metadata model.


Let's take again our previous resource and ask for the identifiers, the spatial WKT and the publication date

.. code-block:: console

    opensearch-client -f atom -p q=processing -p bbox=60,-30,70,-20 "https://catalog.terradue.com/mrossi/search?format=json&q=processing&bbox=60,-30,70,-20" identifier,wkt,published


