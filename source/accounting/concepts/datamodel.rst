.. _accountingdatamodel:

Accounting data model
^^^^^^^^^^^^^^^^^^^^^

The accounting data model is the representation of :ref:`quantities <quantity>` in documents. Generally, one or more quantity is represented by a document that will be registered in the accounting system.

This section describes and list the mandatory and optional elements of a quantity document.

Quantity document structure
"""""""""""""""""""""""""""

Here is an example or usage document. It represents the quantities of resources used for a WPS job submitted by a user. We can tell the job used 15 minutes of CPU, 2.5Gb of memory, intantiated 1 processor and processed 2Mb of data. Of course, this is an arbitrary set of quantities that the WPS service provider decided to account. He could have decided to account only for CPU and data volume.

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


Let's see the different elements of the document.

* **id** *mandatory* : this is the **unique identifier** of the document. The quantities are accounted with that identifier. This means that 2 documents with the same cannot exists in the accounting system. The second document with the same id will not be accepted.
* **account** *mandatory* : This is the parent element for the information relative to the platform for which the quantitites are accounted.
* **account.platform** *mandatory* : This is the identifier of the platform. Every platform has a unique identifier defined.
* **account.username** *mandatory* : This is the identifier of the user on the platform.
* **account.ref** *optional* : This is the platform reference for which the quantities are accounted. This reference identifies an operation type on the platform that is then used for the credit/billing mechanism in order to link the quantities to the operation and apply an eventual rate.
* **compound** *optional* : this is the :ref:`compound` for which the quantities ar accounted. As explained in the terminology, the compound is a human understandable item in which the system can aggregate the quantities. In this case, the compound is a WPS job. The information contained in this element have an informational purpose. Indeed, when the accounting will be reported to a user, it should be readable. The report will likely aggregate the quantities into a rational item defined by the compound when available.
* **compound.id** *mandatory* : This is the unique identifier of the compound. Several documents may use the same compound identifier for aggregating multiple quantities into it.
* **compound.name** *optional* : This is the compound name or reference for the quantities recorded.
* **compound.type** *optional* : This element describes the type of compound. This can be used by the system to make a higher level aggregation of quantities. For instance, for aggregating all the quantities for WPS operation.
* **compound.any** *optional* : This is a container for any additional name/value pair. It can be used for advanced account reporting.
* **hostname** *optional* : This element defines the hostname of the system linked with the usage. This element is informational and used as filter for analytics.
* **timestamp** *optional* : This element defines the time of the usage of the resources. It is also informational for the user reporting (e.g. job completion). The effective time of the quantities accounting is the document submission time.
* **status** *optional* : This element defines the status of the document. It allows 3 values : "TEST", "NOMINAL", "DEGRADED". This important element gives an indicator on the relevancy of the document for a further credit/billing mechanism.
* **location** *optional* : This element allows to geotag a quantity for analytics purpose.
  



.. warning:: Important remarks about the platform reference

  * The platform reference is a way of double checking that quantities accounted correspond to an operation from the platform. This check on currently done only for WPS job submission. See the section :ref:`Execute Operation <processexecuteoperation>` of the Production API to find how this reference is passed.
  * As seen in the example, you can submit many resources quantities in a single document. However, the quantities MUST be grouped by platform reference if any. If, for a specified reference, the quantities are meaningless, the credit/billing mechanism on the platform could not be completed and the quantity could not be taken into account.
  * On the other hand, if quantities are submitted without a platform reference if that latter passed one when it triggered the operation, the credit/billing mechanism on the platform could be refused and the quantity could not be taken into account.







