.. _opensearch:

OpenSearch
^^^^^^^^^^


What is OpenSearch ?
""""""""""""""""""""


OpenSearch is a collection of simple formats for the sharing of search results.
The `OpenSearch <http://www.opensearch.org/Specification s/OpenSearch/1.1/Draft_5>`_ specification defines description document (OSDD) format that can be used to describe a search engine so that it can be used by search client applications.
The OpenSearch response elements can be used to extend existing syndication formats, such as RSS and Atom, with the extra :ref:`metadata <metadata model>` needed to return search results.

Description of Service
""""""""""""""""""""""

The client uses the OSDD to learn about the public interface of the server. The OSDD contains parameterized URL templates that indicate how the search client should make search requests. The URL template can iterate as many times as the output format of the search result are supported.

.. code-block:: xml

    <OpenSearchDescription xmlns="http://a9.com/-/spec/opensearch/1.1/" xmlns:os="http://a9.com/-/spec/opensearch/1.1/" xmlns:atom="http://www.w3.org/2005/Atom" xmlns:time="http://a9.com/-/opensearch/extensions/time/1.0/" xmlns:geo="http://a9.com/-/opensearch/extensions/geo/1.0/" xmlns:eo="http://a9.com/-/opensearch/extensions/eo/1.0/" xmlns:param="http://a9.com/-/spec/opensearch/extensions/parameters/1.0/" xmlns:dc="http://purl.org/dc/elements/1.1/">
      ...
      <description>This service is ...</description> ...
      <Url type="application/atom+xml" rel=”results” template="http://...search/atom?q={searchTerms}&ts={time:start}&te={time:end }"/>
      <Query role="example" searchTerms=”water" time:start="2012-04-01" time:end="2012-06-30”/>
      ...
    </OpenSearchDescription>


Search
""""""

A client constructs the request URL by replacing each {xxx} in the URL template with a value and sends it to the server via HTTP GET. For example :

.. code-block:: console

    <Url type="text/html" template="http://...search?q={searchTerms}&ts={time:start}&te={time:end?}>

can become something like :

.. code-block:: console

    http://...search?q=water&ts=2012-04-01&te=2012-06-30

to be a valid search request string. Optional parameters indicated with a "?" such as {xxx?} can be left empty.


Search Response
"""""""""""""""

OpenSearch doesn’t define or require any specific encoding :ref:`format <mediatype>` for the search response. Instead, it defines a set of search-related metadata elements which can be inserted into existing encoding formats. Typically, list-based XML syndication formats - such as RSS 2.0 and Atom 1.0 - are used.

The OpenSearch response elements include :

+--------------+-------------------------------------------------------------+
| totalResults | number of total results                                     |
+--------------+-------------------------------------------------------------+
| startIndex   | index number corresponding to the first entry item returned |
+--------------+-------------------------------------------------------------+
| itemsPerPage | number of results returned                                  |
+--------------+-------------------------------------------------------------+
| Query        | search query to get the same search response                |
+--------------+-------------------------------------------------------------+

Below is an example of a search response in Atom, to the free keyword “water”. Notice the three OpenSearch elements appear inside the feed element.
 
.. code-block:: xml

    <feed xmlns=http://www.w3.org/2005/Atom xmlns:os=”http://a9.com/-/spec/opensearch/1.1/”>
      <title>OpenSearch response to” water”</title>
      <id>http://example.ceos.org/search?q=water</id>
      <author><name>Taro Yamada</name></author>
      <os:totalResults>231</os:totalResults>
      <os:startIndex>51</os:startIndex>
      <os:itemsPerPage>50</os:itemsPerPage>
      <os:Query role=”request” searchTerms=”water” time:start=”2012-04-01” time:end=”2012-06-30” />
      <entry>
        <title>Water Resource Management Guideline</title> <id>http://aaa.ceos.org/waterResource/guideline/v001</id>
        <link href=”http://aaa.ceos.org/waterResource/guideline/v001“/>
      </entry>
      <entry>
        ...
      </entry>
      <entry>
        ...
      </entry>
      <entry>
        ... 
      </entry>
    </feed>

    