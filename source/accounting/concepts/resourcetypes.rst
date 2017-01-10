.. _resourcetypes:

Resources
^^^^^^^^^

The proposed data model allows to define arbitrary resource types, but we recommend to stick to the following pre-defined ones for ensuring a proper aggregation of the resource usage accounting.

+--------------------------+---------------------------------------------------------+--------------+-----------------------+
| Resource                 | Description                                             | Unit         | Identifier            |
+==========================+=========================================================+==============+=======================+
| CPU                      | Time of CPU processing                                  | milliseconds | CPU_MILLISECONDS      |
+--------------------------+---------------------------------------------------------+--------------+-----------------------+
| Memory                   | Physical memory allocated                               | MegaByte     | PHYSICAL_MEMORY_BYTES |
+--------------------------+---------------------------------------------------------+--------------+-----------------------+
| Filesystem bytes read    | Number of bytes read by filesystem                      | Byte         | BYTE_READ             |
+--------------------------+---------------------------------------------------------+--------------+-----------------------+
| Filesystem bytes written | Number of bytes written by filesystem                   | Byte         | BYTE_WRITTEN          |
+--------------------------+---------------------------------------------------------+--------------+-----------------------+
| Configuration            | Usage time of a given configuration (Typically a VM)    | milliseconds | VM_MILLISECONDS       |
+--------------------------+---------------------------------------------------------+--------------+-----------------------+
| Network out              | Number of bytes downloaded                              | Byte         | NETWORK_OUT           |
+--------------------------+---------------------------------------------------------+--------------+-----------------------+
| Network in               | Number of bytes uploaded                                | Byte         | NETWORK_IN            |
+--------------------------+---------------------------------------------------------+--------------+-----------------------+
| Processor                | Number of instantiation for an algorithm                | Integer      | PROC_INSTANCE         |
+--------------------------+---------------------------------------------------------+--------------+-----------------------+
| Data Volume              | Number of bytes of data processed (input and/or output) | Byte         | PROC_VOLUME_BYTES     |
+--------------------------+---------------------------------------------------------+--------------+-----------------------+
| Request                  | Number of request to a system                           | Integer      | NUM_REQ               |
+--------------------------+---------------------------------------------------------+--------------+-----------------------+


