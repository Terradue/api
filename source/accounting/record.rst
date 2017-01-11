.. _recordaccounting :


Record
------

This part describes how to add accoutning records in the accounting system of practical usage from the platform.

Every document presented in the following sections are recorded to the accouting system by posting them using HTTP REST API

.. code-block:: console
    
        curl -XPOST -H "Content-Type: application/json" -u username:password -d@doc.json https://usage.terradue.com/accounting/partners/acme/quantity/record


.. _recordprocaccounting :

Processing from a WPS JOB
^^^^^^^^^^^^^^^^^^^^^^^^^

When the platform triggers a WPS job, it is an instance of a processing service registered on the portal. This latter submits a WPS job with a reference. See the section :ref:`Execute Operation <processexecuteoperation>` of the Production API to find how this reference is passed.

When the job is completed. The processing system shall record quantities for the processing done. Here is the already described example from the section :ref:`accountingdatamodel`.

.. code-block:: javascript

    {
      "id" : "t2cp_cluster5342_application_1479400262723_8995",
      "account" : {
        "platform": "urban-tep",
        "username": "emathot",
        "ref": "1738ad7b-534e-4aca-9861-b26fb9c0f983"
      }
      "compound": {
        "id": "t2cp_cluster5342_oozie_0004218-161117173256693-oozie-oozi-W",
        "name": "oozie:action:ID=0004218-161117173256693-oozie-oozi-W"
        "type": "WPS-OOZIE"
        "any": {
          "jobid": "oozie:action:T=map-reduce:W=t2-subset-snap:A=streaming-8247:ID=0004218-161117173256693-oozie-oozi-W"
        }
      },
      "quantity" : [
        {
          "id": "CPU_MILLISECONDS",
          "value": 900000
        },
        {
          "id": "PHYSICAL_MEMORY_BYTES",
          "value": 2684354560
        },
        {
          "id": "PROC_INSTANCE",
          "value": 1
        },
        {
          "id": "PROC_VOLUME_BYTES",
          "value": 2097152
        }
      ]
      "hostname": "cloud.terradue.com",
      "timestamp": "2017-01-10T10:32:16Z",
      "status": "TEST",
      "location": {
        "coordinates": [
          9.491,
          51.2993
        ],
      }
    }




It represents the quantities of resources used for a WPS job submitted by a user. We can tell the job used 15 minutes of CPU, 2.5Gb of memory, intantiated 1 processor and processed 2Mb of data. Of course, this is an arbitrary set of quantities that the WPS service provider decided to account. He could have decided to account only for CPU and data volume. Nevertheless, this document may not contain all the quantities used by the job and one or more documents could be recorded to complete the accounting. For instance, if the WPS job would trigger a 2 step processing, the processing provider would record this second document.

.. code-block:: javascript

    {
      "id" : "t2cp_cluster5342_application_1479400262723_8996",
      "account" : {
        "platform": "urban-tep",
        "username": "emathot",
        "ref": "1738ad7b-534e-4aca-9861-b26fb9c0f983"
      },
      "compound": {
        "id": "t2cp_cluster5342_oozie_0004218-161117173256693-oozie-oozi-W",
        "name": "oozie:action:ID=0004218-161117173256693-oozie-oozi-W"
        "type": "WPS-OOZIE"
        "any": {
          "jobid": "oozie:action:T=map-reduce:W=t2-snap-classification:A=streaming-760f:ID=0002692-161117173256693-oozie-oozi-W"
        }
      },
      "quantity" : [
        {
          "id": "CPU_MILLISECONDS",
          "value": 15323300
        },
        {
          "id": "PHYSICAL_MEMORY_BYTES",
          "value": 4688952360
        },
        {
          "id": "PROC_VOLUME_BYTES",
          "value": 654894165
        }
      ]
      "hostname": "cloud.terradue.com",
      "timestamp": "2017-01-10T10:50:34Z",
      "status": "TEST",
      "location": {
        "coordinates": [
          9.491,
          51.2993
        ],
      }
    }



In this second document, the id has changed (very important) and this time, no processor instantiation is accounted. Please note that the document still references the account reference that allows the platform to retrieve the original service on the portal and apply the credit/billing mechanism.

.. _recorddataaccounting :

General Data usage
^^^^^^^^^^^^^^^^^^

The following document records quantities of data requested on the storage repository : 2Gb read and downloaded by the user.

.. code-block:: javascript

    {
      "id" : "t2cp_store_scihub_20170110105425547",
      "account" : {
        "platform": "t2cp",
        "username": "emathot"
      }
      "compound": {
        "id": "t2cp_store_scihub",
        "name": "scihub-cache:sentinel1/GRD/2016/10/31/files/v1/S1A_IW_GRDH_1SDV_20161031T185711_20161031T185740_013738_0160C3_1851.zip"
        "type": "STORE-REPO"
      },
      "quantity" : [
        {
          "id": "BYTE_READ",
          "value": 911799157
        },
        {
          "id": "NETWORK_OUT",
          "value": 911799157
        }
      ]
      "hostname": "store.terradue.com",
      "timestamp": "2017-01-10T10:54:25Z",
      "status": "TEST",
      "location": {
        "coordinates": [
          9.491,
          51.2993
        ],
      }
    }



.. note:: In this case, there is no specific reference to an operation on the platform. The quantities are accounted as general usage of the platform but we could also record the data usage linked to the previous WPS job. For that purpose, the document must add the platform operation reference in "account.ref" as in the previous examples.


.. _recordcatalogueaccounting :

Catalogue request
^^^^^^^^^^^^^^^^^

The following document records quantities of dataset posted to the catalogue. In this case the user registered 123 new datasets.

.. code-block:: javascript

    {
      "id" : "t2cp_catalog_emathot_20170110105425547",
      "account" : {
        "platform": "t2cp",
        "username": "emathot"
      }
      "compound": {
        "id": "t2cp_catalog_emathot",
        "name": "https://catalog.terradue.com/emathot"
        "type": "CATALOG-INDEX-POST"
      },
      "quantity" : [
        {
          "id": "NUM_REQ",
          "value": 123
        }
      ]
      "hostname": "catalog.terradue.com",
      "timestamp": "2017-01-10T10:54:25Z",
      "status": "TEST",
      "location": {
        "coordinates": [
          9.491,
          51.2993
        ],
      }
    }


