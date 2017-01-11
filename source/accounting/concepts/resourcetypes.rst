.. _resourcetypes:

Resources
^^^^^^^^^

The proposed data model allows to define arbitrary resource types, but we recommend to stick to the following pre-defined ones for ensuring a proper aggregation of the resource usage accounting.

+--------------------+--------------------------------------+--------------+-----------------------+
| Resource           | Description                          | Unit         | Identifier            |
+====================+======================================+==============+=======================+
| CPU                | Time of CPU processing               | milliseconds | CPU_MILLISECONDS      |
+--------------------+--------------------------------------+--------------+-----------------------+
| Memory             | Physical memory allocated            | MegaByte     | PHYSICAL_MEMORY_BYTES |
+--------------------+--------------------------------------+--------------+-----------------------+
| Filesystem read    | Number of bytes read                 | Byte         | BYTE_READ             |
|                    | by filesystem                        |              |                       |
+--------------------+--------------------------------------+--------------+-----------------------+
| Filesystem written | Number of bytes written              | Byte         | BYTE_WRITTEN          |
|                    | by filesystem                        |              |                       |
+--------------------+--------------------------------------+--------------+-----------------------+
| Configuration      | Usage time of a given                | milliseconds | VM_MILLISECONDS       |
|                    | configuration (Typically a VM)       |              |                       |
+--------------------+--------------------------------------+--------------+-----------------------+
| Network out        | Number of bytes downloaded           | Byte         | NETWORK_OUT           |
+--------------------+--------------------------------------+--------------+-----------------------+
| Network in         | Number of bytes uploaded             | Byte         | NETWORK_IN            |
+--------------------+--------------------------------------+--------------+-----------------------+
| Processor          | Number of instantiation              | Integer      | PROC_INSTANCE         |
|                    | for an algorithm                     |              |                       |
+--------------------+--------------------------------------+--------------+-----------------------+
| Data Volume        | Number of bytes of                   | Byte         | PROC_VOLUME_BYTES     |
|                    | data processed (input and/or output) |              |                       |
+--------------------+--------------------------------------+--------------+-----------------------+
| Request            | Number of request to a system        | Integer      | NUM_REQ               |
+--------------------+--------------------------------------+--------------+-----------------------+


