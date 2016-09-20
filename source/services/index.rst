
Service API
===========


The Service API covers many use cases for the usage of the processing service of the platform. They are described in the following diagram.

.. uml::
  :caption: Services API use cases

   !include includes/skins.iuml

   skinparam backgroundColor #FFFFFF
   skinparam componentStyle uml2

   actor User

   rectangle user {
     (Discover Providers) as UCDP
     User -> UCDP
     (Describe Services) as UCDS
     User -> UCDS
     (Execute Process) as UCEP
     User -> UCEP
   }

   actor Provider

   rectangle provider {
     (Register as a Provider) as UCRP
     UCRP <- Provider
     (Expose Services) as UCES
     UCES <- Provider
     (Deliver Results) as UCDR
     UCDR <- Provider
   }

   UCDP .. UCRP
   UCDS .. UCES
   UCEP .. UCDR


As shown in previous diagram they are mainly 2 actors:

- **Service User** that discovers the service Available via the portal API,
- **Service Provider** that promote services and deliver processing results via the portal API.



.. toctree::
   :maxdepth: 2

   providerdiscovery
   servicedescription
   processexecution
   providerregister
   servicesexposition
   resultdelivery
   

