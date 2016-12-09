.. _terminology:

Terminology
^^^^^^^^^^^

.. _cluster:

Data Cluster
""""""""""""

A data cluster is a collection of one or more nodes (servers) that together brings an instance of the :ref:`data agency <dataagency>` and holds your entire documents and data. It provides federated indexing and search capabilities across all nodes. A cluster is identified by its host name. The prime data cluster is ``data.terradue.com`` and all the tools uses it by default.


.. _catalogue:

Catalogue
"""""""""

In the :ref:`Data Agency <dataagency>`, this is the module that hosts the service to index, search, update, and delete :ref:`entries <entry>` in several indexes.


.. _index:

Index
"""""

An index is a collection of :ref:`entries <entry>` in the :ref:`catalogue` that most of the time describe a :ref:`dataset <dataset>`. For example, there is an index for Sentinel-1 data, another index for Landsat-8 data, and yet another index for your own data. An index is identified by a name (that must be all lowercase) and this name is used to refer to the index when performing indexing, search, update, and delete operations against the entries in it. Index names are unique in the :ref:`cluster <cluster>` where they are hosted.

.. _type:


Type
""""

Within an index, the :ref:`entries <entry>` are defined by one type. A type is a logical category/partition of your index whose semantics is defined according to a :ref:`metadata model <metadatamodel>`. In general, a type is defined for entries that have a set of common properties. One of the common type is ``Geo&Time`` that specifies spatial and temporal properties for an entry.


.. _entry:

Entry
"""""

An entry is the basic object indexed in the catalogue. Each entry has a unique identifier in an index. The other properties are specific to the :ref:`type` that structures the entry. 


.. note:: A set of one or more entries is always represented in a feed (e.g. Atom).


.. _collection:

Collection
""""""""""

A collection is a **reference** to an abstract set of :ref:`entries <entry>` sharing one or more properties. A collection typically references a :ref:`series <series>` in an :ref:`index <index>` in the catalogue or a :ref:`data package <datapackage>` in the portal.


.. _series:

Series
""""""

A series is a set of :ref:`entries <entry>` in the same :ref:`index <index>` with the same :ref:`type <type>` with predifined query filters. For instance, a series "SLC" in index sentinel1 will be all the enties in the index with the product type equals to "SLC".


.. _datapackage:

Data Package
""""""""""""

A data package is a set of :ref:`entries <entry>` selected by the user on the portal.


.. _storage:

Storage
"""""""

In the :ref:`Data Agency <dataagency>`, this is the module that hosts the service to upload, download and delete data in the :ref:`repositories <repository>`.


.. _repository:

Repository
""""""""""

This is the storage unit for uploading and downloading data files to/from the :ref:`storage`. As per the indices, there is a repository for Sentinel-1 data, another index for Landsat-8 data, and yet another index for your own data. A repository is identified by a name (that must be all lowercase) and this name is used to refer to the repository when performing upload, download and delete operations against the data files in it. Repository names are unique in the cluster where they are hosted. 

There are 3 types of repositories:

  - **Local** repository: It is a storage unit where data are located on the :ref:`cluster`. this is the usual type of repository for users, groups or community laboratories,
  - **Remote** repository: It acts as a proxy for another third-party data source and abstract the access to this source as a repository,
  - **Virtual** repository: This is an aggregation of any types of repository in a single one.


.. _dataset:

Dataset
"""""""

A datset is a set of one or more data files in a repository. Each dataset is stored in a directory on the repository and are organised as in a file system.



Index and Repository Relationship
"""""""""""""""""""""""""""""""""

Indices and repositories names are usually linked, they are associated. The entries indexed in ``sentinel1`` index describe the data stored in ``sentinel1`` repository. There is usually one :ref:`entry` describing a :ref:`dataset`.


