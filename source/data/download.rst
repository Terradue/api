.. _download :


Download
--------

This part describes how to manage the download resource location of a dataset indexed in the catalogue and then use the data agency function for different purposes



Direct download
^^^^^^^^^^^^^^^

Every entry in an index of the catalogue can have a link to the data that it describes. There is a resource location (URL) also called :ref:`enclosure <createentries>` that can be associated in the :ref:`entry metadata <createentries>`. This URL can be extracted easily using opensearch-client. For instance,

.. code-block:: console

    opensearch-client -p do= "https://catalog.terradue.com/sentinel1/search" enclosure


.. note:: Please note the parameter ``do=`` that indicates to the catalogue to **NOT** apply any :ref:`delegate download <delegatedownload>`.



.. _delegatedownload :

Delegate Download
^^^^^^^^^^^^^^^^^

We just saw how to simply extract the enclosure of an entry. With the parameter :ref:`downloadOrigin` (``do=``) the catalogue do not perform any change on the original enclosure link of the entry. However, by default and if the catalogue provides with the :ref:`downloadOrigin` parameter, the opensearch-client set automatically the hostname of the machine in this parameter. If the same command as above is performed like this on machine ``sandbox1.dev.terradue.int``

.. code-block:: console

    opensearch-client "https://catalog.terradue.com/sentinel1/search" enclosure


the catalogue is queried as follow


.. code-block:: console

    https://catalog.terradue.com/sentinel1/search?do=sandbox1.dev.terradue.int


This information allows the catalogue to apply a filter on the results and eventually modify the enclosure link of the entries. If the download origin is elligible to the **data gateway proxy download**, then the enclosure shall point to the closest data gateway to provide the data access via the best route.


.. _datagatewayproxydl :


Data Gateway Proxy Download
^^^^^^^^^^^^^^^^^^^^^^^^^^^

If the resource location returned by the catalogue points to a data gateway like

.. code-block:: console

    https://store.terradue.com/download/sentinel1/files/v1/S1A_IW_SLC__1SDH_20160915T090555_20160915T090624_013061_014B4B_4793


then the download is performed via the Data Gateway that enables many function such as caching to allow the best download performance of the data requested.


.. warning:: Please be aware that the Data Gateway Proxy Download may take some time to start dependeng of the configuration of the repository from which you perform the download. Indeed, the data gateway may be required to perform :ref:`implicitcaching` before delivering the data.








