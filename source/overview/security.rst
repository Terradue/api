.. _security :

Security
--------

.. _authorizationscheme :

Authorization scheme
^^^^^^^^^^^^^^^^^^^^

The following class diagram describes the authorization scheme applied in platform providing with the access control mechanism to the resources provided by the platform.

.. uml::
  :caption: Authorisation Scheme Class Diagram
  :align: center

  !include includes/skins.iuml

   skinparam backgroundColor #FFFFFF
   skinparam componentStyle uml2
  
          Group  *-right-"0..*" User : has >
          User -down-"0..*" Domain : belongs >
          Group -down-"0..*" Domain : belongs >
          abstract class Resource
          Resource -- ResourceType : is specified by >
          ResourceType -right- Privilege : defines >
          Role *-down- Privilege : is granted >
          class Permission
          User -- Resource : accesses >
          Group -- Resource : accesses >
          Resource -right-"0..1" Domain : belongs >
  
          (User, Domain) . Role
          (Group, Domain) . Role
          (User, Resource) . Permission
          (Group, Resource) . Permission
  
  

The following defintions supports this scheme:

- **User** and **Group** are defined according the regular convention that a group is a set of users.
- A **Domain** is an organizational unit to regroup **User**, **Group** and **Resources**.
- A **Role** defines the set of **Privileges** that are granted to a **User** or a **Group** for a specific **Domain** or globally.
- The assignement of a **Role** to a **User** or a **Group** is called a "**Role Grant**". A **Role Grant** can be associated to a **Domain** and is therefore called "**Domain Role Grant**". A **Role Grant** taht is not associated to any **Domain** is a "**Global Role Grant**".
- A **Resource** can belong to a **Domain**. If not, the **Resource** is considered as global.
- A **Privilege** is an access control for a given **Resource Type**.
- A **Permission** is a specific **Privilege** for a **User** or a **Group** for a given **Resource**. 

And the following rules applies:

- **Users** and **Groups** with a **Domain Role Grant** on a certain **Domain** have all the **Privileges** defined by that **Role** on all **Resources** belonging to that **Domain**.
- **Users** and **Groups** with a **Global Role Grant** have all the **Privileges** defined by that **Role** on all **Resources** of that **Resource Type**, whether belonging to a **Domain** or not.
- A specific **Permission** for a specific **Resource** is granted to a specific **User** or **Group**.

The authorisation consists of two phases:

- a generic phase where the current User 's access privileges are compared to the necessary privileges for the accessed object according to the domain or the global.
- an optional specific phase where the same check is performed for the requested operation. This phase is specific to the entity object in question as the possible operations are entity-specific.

The authorisation for a specific operation must be ensured by the code of the Entity object. The central authorisation model supports this task by initialising the properties corresponding to the operation privilege that are applicable to the entity subclass.

.. _roleprivperm :


Role, Privileges and Permissions
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Basic Privileges
""""""""""""""""

For all resources, there are 6 basic privileges and permisions: "Can Create", "Can Change", "Can Delete", "Can View", "Can Search" and "Can Manage".
The following table describes the access to a :ref:`resource type <resources>` for a given privilege according to the software component providing the service.
If a combination is not listed then no access is granted.

+--------------------------+-------------------------------+----------------------------------------------------------------------------------------------------------------+
| Resource                 | Privilege                     | description                                                                                                    |
+==========================+===============================+================================================================================================================+
| :ref:`catalogue`         | Can View                      | Allow discovering the :ref:`indices <index>` present in the :ref:`catalogue`                                   |
+--------------------------+-------------------------------+----------------------------------------------------------------------------------------------------------------+
| :ref:`catalogue`         | Can Manage                    | Allow Modifying global configuration element of the catalogue                                                  |
+--------------------------+-------------------------------+----------------------------------------------------------------------------------------------------------------+
| :ref:`collection`        | Can Create                    | In the portal, allow creating a new collection                                                                 |
+--------------------------+-------------------------------+----------------------------------------------------------------------------------------------------------------+
| :ref:`collection`        | Can Change                    | In the portal, allow modifying an existing collection                                                          |
+--------------------------+-------------------------------+----------------------------------------------------------------------------------------------------------------+
| :ref:`collection`        | Can Delete                    | In the portal, allow delete an existing collection                                                             |
+--------------------------+-------------------------------+----------------------------------------------------------------------------------------------------------------+
| :ref:`collection`        | Can View                      | In the portal, allow viewing an existing collection                                                            |
+--------------------------+-------------------------------+----------------------------------------------------------------------------------------------------------------+
| :ref:`collection`        | Can Search                    | In the portal, allow searching for an existing collection [CanView]                                            |
+--------------------------+-------------------------------+----------------------------------------------------------------------------------------------------------------+
| :ref:`collection`        | Can Manage                    | In the portal, allow granting privilege and permissions for an existing collection [CanView&CanChange]         |
+--------------------------+-------------------------------+----------------------------------------------------------------------------------------------------------------+
| :ref:`datapackage`       | Can Create                    | In the portal, allow creating a new data package                                                               |
+--------------------------+-------------------------------+----------------------------------------------------------------------------------------------------------------+
| :ref:`datapackage`       | Can Change                    | In the portal, allow modifying an existing data package                                                        |
+--------------------------+-------------------------------+----------------------------------------------------------------------------------------------------------------+
| :ref:`datapackage`       | Can Delete                    | In the portal, allow delete an existing data package                                                           |
+--------------------------+-------------------------------+----------------------------------------------------------------------------------------------------------------+
| :ref:`datapackage`       | Can View                      | In the portal, allow viewing an existing data package                                                          |
+--------------------------+-------------------------------+----------------------------------------------------------------------------------------------------------------+
| :ref:`datapackage`       | Can Search                    | In the portal, allow searching for an existing data package [CanView]                                          |
+--------------------------+-------------------------------+----------------------------------------------------------------------------------------------------------------+
| :ref:`datapackage`       | Can Manage                    | In the portal, allow granting privilege and permissions for an existing data package [CanView&CanChange]       |
+--------------------------+-------------------------------+----------------------------------------------------------------------------------------------------------------+
| :ref:`dataset`           | inherited form the parent     |                                                                                                                |
|                          | :ref:`repository`             |                                                                                                                |
+--------------------------+-------------------------------+----------------------------------------------------------------------------------------------------------------+
| :ref:`entry`             | inherited form the parent     |                                                                                                                |
|                          | :ref:`index` or :ref:`series` |                                                                                                                |
+--------------------------+-------------------------------+----------------------------------------------------------------------------------------------------------------+
| :ref:`index`             | Can Create                    | In the catalog, allow creating a new index (other than personal index)                                         |
+--------------------------+-------------------------------+----------------------------------------------------------------------------------------------------------------+
| :ref:`index`             | Can Change                    | In the catalog, allow modifying an existing index (other than personal index)                                  |
+--------------------------+-------------------------------+----------------------------------------------------------------------------------------------------------------+
| :ref:`index`             | Can Delete                    | In the catalog, allow deleting an existing index (other than personal index)                                   |
+--------------------------+-------------------------------+----------------------------------------------------------------------------------------------------------------+
| :ref:`index`             | Can View                      | In the catalog, allow viewing an existing index (other than personal index)                                    |
+--------------------------+-------------------------------+----------------------------------------------------------------------------------------------------------------+
| :ref:`index`             | Can Search                    | In the catalog, allow searching for an existing index (other than personal index) [CanView]                    |
+--------------------------+-------------------------------+----------------------------------------------------------------------------------------------------------------+
| :ref:`index`             | Can Manage                    | In the catalog, allow granting privilege and permissions for an existing index                                 |
|                          |                               | [CanView&CanChange] (other than personal index)                                                                |
+--------------------------+-------------------------------+----------------------------------------------------------------------------------------------------------------+
| :ref:`job`               | Can Create                    | In a sandbox or cluster, allow executing a new job from a process                                              |
+--------------------------+-------------------------------+----------------------------------------------------------------------------------------------------------------+
| :ref:`job`               | Can Delete                    | In a sandbox or cluster, allow deleting an exisitng job                                                        |
+--------------------------+-------------------------------+----------------------------------------------------------------------------------------------------------------+
| :ref:`job`               | Can View                      | In a sandbox or cluster, allow viewing the status or the results of a job                                      |
+--------------------------+-------------------------------+----------------------------------------------------------------------------------------------------------------+
| :ref:`job`               | Can Search                    | In a sandbox or cluster, allow searching for an existing job                                                   |
+--------------------------+-------------------------------+----------------------------------------------------------------------------------------------------------------+
| :ref:`Process`           | inherited form the parent     |                                                                                                                |
|                          | :ref:`processingservice`      |                                                                                                                |
+--------------------------+-------------------------------+----------------------------------------------------------------------------------------------------------------+
| :ref:`processingservice` | Can Create                    | In the portal, allow creating a new processing service                                                         |
+--------------------------+-------------------------------+----------------------------------------------------------------------------------------------------------------+
| :ref:`processingservice` | Can Change                    | In the portal, allow modifying an existing processing service                                                  |
+--------------------------+-------------------------------+----------------------------------------------------------------------------------------------------------------+
| :ref:`processingservice` | Can Delete                    | In the portal, allow delete an existing processing service                                                     |
+--------------------------+-------------------------------+----------------------------------------------------------------------------------------------------------------+
| :ref:`processingservice` | Can View                      | In the portal, allow viewing an existing processing service                                                    |
+--------------------------+-------------------------------+----------------------------------------------------------------------------------------------------------------+
| :ref:`processingservice` | Can Search                    | In the portal, allow searching for an existing processing service [CanView]                                    |
+--------------------------+-------------------------------+----------------------------------------------------------------------------------------------------------------+
| :ref:`processingservice` | Can Manage                    | In the portal, allow granting privilege and permissions for an existing processing service [CanView&CanChange] |
+--------------------------+-------------------------------+----------------------------------------------------------------------------------------------------------------+
| :ref:`repository`        | Can Create                    | In the storage, allow creating a new dataset                                                                   |
+--------------------------+-------------------------------+----------------------------------------------------------------------------------------------------------------+
| :ref:`repository`        | Can Change                    | In the storage, allow annotating an existing dataset                                                           |
+--------------------------+-------------------------------+----------------------------------------------------------------------------------------------------------------+
| :ref:`repository`        | Can Delete                    | In the storage, allow overwriting/delete an existing dataset                                                   |
+--------------------------+-------------------------------+----------------------------------------------------------------------------------------------------------------+
| :ref:`repository`        | Can View                      | In the storage, allow reading an existing dataset                                                              |
+--------------------------+-------------------------------+----------------------------------------------------------------------------------------------------------------+
| :ref:`repository`        | Can Manage                    | In the storage, allow granting privilege and permissions for an existing dataset [CanView&CanChange]           |
+--------------------------+-------------------------------+----------------------------------------------------------------------------------------------------------------+
| :ref:`series`            | Can Create                    | In the catalog, allow creating a new series (other than personal index)                                        |
+--------------------------+-------------------------------+----------------------------------------------------------------------------------------------------------------+
| :ref:`series`            | Can Change                    | In the catalog, allow modifying an existing series (other than personal index)                                 |
+--------------------------+-------------------------------+----------------------------------------------------------------------------------------------------------------+
| :ref:`series`            | Can Delete                    | In the catalog, allow deleting an existing series (other than personal index)                                  |
+--------------------------+-------------------------------+----------------------------------------------------------------------------------------------------------------+
| :ref:`series`            | Can View                      | In the catalog, allow viewing an existing series (other than personal index)                                   |
+--------------------------+-------------------------------+----------------------------------------------------------------------------------------------------------------+
| :ref:`series`            | Can Search                    | In the catalog, allow searching for an existing series (other than personal index) [CanView]                   |
+--------------------------+-------------------------------+----------------------------------------------------------------------------------------------------------------+
| :ref:`series`            | Can Manage                    | In the catalog, allow granting privilege and permissions for an existing series                                |
|                          |                               | [CanView&CanChange] (other than personal index)                                                                |
+--------------------------+-------------------------------+----------------------------------------------------------------------------------------------------------------+

Basic domains & roles
"""""""""""""""""""""

Keep in mind that the aboved table describe only the privileges, they are most of the ime combined with a role in a domain.

Some domains are automatically created based on users, their organizations and their objectives on the platform:

- One **domain** is created for every new **user** registered on the platform with an access to The Terradue Cloud Platform.
- One **domain** is created for any **organisation** represented on the platform that provides with data, processor or ICT resources.
- One **domain** is created for every **laboratory** in which a processing service is integrated. A laboratory is often the same domain as the organization but sometimes, it may englobe many of them or a subset depending on the project scope.


When combined in a role and a domain, the included user or the group have different level of access to the resource. The following table lists the most basic combination implemented on the platform.

+---------------+----------------------------+-------------------------+---------------------------------------+----------------------------------------------------------------------------------------+
| Role          | Domain(s)                  | Privilege(s)            | User(s) and group(s)                  | Resources                                                                              |
+===============+============================+=========================+=======================================+========================================================================================+
| Owner         | username                   | All                     | User with the corresponding username  | :ref:`datapackage`, :ref:`index`, :ref:`repository`, :ref:`series`                     |
+---------------+----------------------------+-------------------------+---------------------------------------+----------------------------------------------------------------------------------------+
| Owner         | organisation               | All                     | User that initiated a community       | :ref:`collection`, :ref:`datapackage`, :ref:`index`, :ref:`repository`, :ref:`series`, |
|               |                            |                         | or a thematic group                   | :ref:`processingservice`                                                               |
+---------------+----------------------------+-------------------------+---------------------------------------+----------------------------------------------------------------------------------------+
| Administrator | all domains in a community | All                     | Portal Administrators                 | :ref:`collection`, :ref:`datapackage`, :ref:`index`, :ref:`repository`, :ref:`series`, |
|               |                            |                         |                                       | :ref:`processingservice`                                                               |
+---------------+----------------------------+-------------------------+---------------------------------------+----------------------------------------------------------------------------------------+
| Content       | all domains in a community | CanView & CanSearch     | Scientific Communicators              | :ref:`collection`, :ref:`datapackage`, :ref:`index`, :ref:`repository`, :ref:`series`  |
| Authority     |                            | & CanCreate & CanDelete |                                       |                                                                                        |
+---------------+----------------------------+-------------------------+---------------------------------------+----------------------------------------------------------------------------------------+
| Member        | organisation               | CanView & CanSearch     | User or group invited in a community  | :ref:`collection`, :ref:`datapackage`, :ref:`index`, :ref:`repository`, :ref:`series`  |
|               |                            |                         | or a thematic group                   |                                                                                        |
+---------------+----------------------------+-------------------------+---------------------------------------+----------------------------------------------------------------------------------------+
| Staff         | organisation               | CanView & CanSearch     | User or group part of an organisation | :ref:`collection`, :ref:`datapackage`, :ref:`index`, :ref:`repository`, :ref:`series`, |
|               |                            | & CanCreate & CanDelete |                                       | :ref:`processingservice`                                                               |
+---------------+----------------------------+-------------------------+---------------------------------------+----------------------------------------------------------------------------------------+
| Expert        | laboratory                 | CanView & CanSearch     | Users that access the Developer       | :ref:`sandbox`                                                                         |
|               |                            | & CanCreate & CanDelete | Cloud Sandbox                         |                                                                                        |
+---------------+----------------------------+-------------------------+---------------------------------------+----------------------------------------------------------------------------------------+


The roles are obviously not limited to the previous list. Any combination of domain and privileges as a new role can be defined in the platform.


