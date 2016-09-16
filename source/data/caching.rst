.. _caching :


Caching
-------

This part describes how to use the advanced functions of caching data in the data gateway.


.. _implicitcaching :

Implicit caching
^^^^^^^^^^^^^^^^

When a data is downloaded via the :ref:`datagatewayproxydl`, there is a chance that the data is cached by the system when you request it. This implicit caching of data is used to improve performance of a likely another download of the same data by you or another user.


Early caching
^^^^^^^^^^^^^

On the other hand, there is the possibility to explicitely request the cache of a specific data in the data gateway in anticipation of a leter usage of this data in a processing. In order to simply ask for the early caching of the data in the system. simply perform a HTTP HEAD on the delegate download url returned by the catalogue

.. code-block:: console

    curl -u mrossi:abcDEF --location-trusted  -L -m 30 -XHEAD https://store.terradue.com/download/sentinel1/files/v1/S1A_IW_SLC__1SDH_20160915T090555_20160915T090624_013061_014B4B_4793



Some curl parametrs here are important to understand:

  - ``-L`` it allows curl to follow redirections. Indeed the data gateway may redirect your download request to another resources or even server according to the best download location.

  - ``--location-trusted`` this instructs curl to allow sending the name + password/api key to all hosts that the site may redirect to. Your request must be always authenticated, even after a redirection.
  
  - ``-m 10`` This optional srgument instructs curl that this operation shall not take more than 10 seconds. If we do not want to wait for the result of the caching, we can use this argument to close the connection to the server after a certain time. The data gateway keeps anyway caching the data.


.. note:: If the request above answers directly with a HTTP 200 response. It means the data is already cached and ready to download.






