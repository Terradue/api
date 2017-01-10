.. _accountingterminology:

Terminology
^^^^^^^^^^^

.. _quantity:

Quantity
""""""""

Quantities represent dimensions of resource consumption and are linked to entity types that represent consumable items such as computing resources or data collections or items for which some sort of licence is due (algorithms).
The kind of resources that can be quantified are listed in the section :ref:`resourcetypes`.


.. _compound:

Compound
""""""""

This is the item representing the container of the quantities for the reporting system. It is then used to filter/aggregate :ref:`quantity` to a specific type of operation. For instance, a same job processing can be made of quantities of CPU time, memory allocation, processor instances and data volume to process. Another example is a data transfer made of multiple disk bytes written and read and network bytes uploaded and downloaded.


.. _account:

Account
"""""""

The account is the set of information identifying the origin of the quntityies accounting. It usually identifies element of the platform originating the operation for which the quantities are accounted. Those information are typically the platform name, the username and an internal reference.



