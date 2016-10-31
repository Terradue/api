.. _productionterminology:

Production Terminology
^^^^^^^^^^^^^^^^^^^^^^

.. _productioncenter:

Production Center
"""""""""""""""""

A production center defines any group of :ref:`productioncluster` setup by any organization for the processing of data.

.. _productioncluster:

Production Cluster
""""""""""""""""""

A production cluster is a collection of one or more nodes (servers) that together brings an instance of the :ref:`production center <productioncenter>` and run :ref:`jobs <job>` of different :ref:`workflows <workflow>` for several users.


.. _processingservice:

Processing Service
""""""""""""""""""

A processing service is an online service to execute processing task hosted by a production center. E.g. WPS is a processing service.


.. _process:

Process
"""""""

A process is a processing workflow that is made avalable via the processing service.


.. _job:

Job
"""

A job is a reference to a generic instance of a :ref:`process` tasked on a :ref:`productioncenter`.



