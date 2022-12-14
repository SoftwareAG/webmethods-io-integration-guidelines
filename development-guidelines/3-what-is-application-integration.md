# 3 What is Application Integration?

Gartner defines application integration as:

> Application integration is the process of enabling independently designed applications to work together. Commonly required capabilities include:
>
> * Keeping separate copies of data (in independently designed applications) consistent
> * Orchestrating the integrated flow of multiple activities performed by disparate applications
> * Providing access to data and functionality from independently designed applications through what appears to be a single user interface or application service
>   https://www.gartner.com/en/information-technology/glossary/application-integration

which is a succinct and accurate definition of what application integration is generally considered to be.

Historically Application integration was facilitated using a self-hosted integration platform that provides capabilities to enable integrations through standards based approaches, or via specific connectors, adapters or bespoke APIs.  These platforms were often implemented in a model known as an __Enterprise Service Bus (ESB)__.
__Note:__ self-hosted is also known as on-premises.

The Enterprise Service Bus is still a valid architectural choice, using platforms such as Software AG's [webMethods Integration Server](https://www.softwareag.com/en_corporate/platform/integration-apis/webmethods-integration.html).  Particularly beneficial when you are trying to connect lots of self-hosted products, and/or products with very bespoke integration requirements.  
ESB implementations were traditionally implemented using a __Service Oriented Architecture (SOA)__ methodology, with a strong focus on
>
> * reuse of services (implementing once)
> * governing the use of services
> * centralizing and canonicalizing data structures

For example, an ESB implemented solution could take data from a source system, transforming it to a pre-defined data structure that represents the business entity (known as a data canonical model), and then publish it to a messaging platform. Messaging subscribers could react to these canonical messages and transform them to the structure of the destination system, and then send the data to the target system using one of ESB functions.

More recently however, application integration has transformed into more modern architectures to suit the needs of organizations, which include:

__Microservice Based Integrations__

> Microservice Based Integrations are Facilitated by Microservice ready integration platforms, such as Software AG's [MicroServices Runtime (MSR)](https://www.softwareag.com/en_corporate/platform/integration-apis/microservices-platform.html), allowing the creation and deployment of microservices, to run at scale, as a part of a microservice architecture, utilizing micro API gateways, service or application meshes and more.  This is an approach suited to the most technical of integration and development teams, but is suitable in particular for cloud scale integration programs.

 __Cloud based integration__

> Cloud based integration is useful when you're trying to interconnect many clouds (typically SaaS) by systems, and most often facilitated by an __Integration Platform As A Service (iPaaS)__, delivering the capabilities as a suite of cloud services. Some iPaaS platforms (such as Software AG's [webMethods.io Integration](https://www.softwareag.com/en_corporate/platform/integration-apis/api-integration-platform.html)) have been designed to support enterprise class integration initiatives.  This may sometimes be termed as Enterprise iPaaS, or __EiPaaS__.  
These offer high availability, disaster recovery, security, SLAs, and capabilities to develop, execute and monitor many integrations scenarios, deliver as a service, with managed upgrades.  In addition, some iPaaS platforms also provide out-of-the-box support for multiple personas, covering the complete spectrum of users, from technical business users (sometimes termed business technologist, citizen integrators, or citizen developers), administrators, integration specialists, and developers, meaning the iPaaS offers capabilities to suite the needs of each of these differing personas, including hundreds of connectors to make it easy to integrate with systems for all skill sets.

__Hybrid Integration__

> This is a typical enterprise implementation style, mixing Cloud based EiPaaS platforms to easily integration SaaS systems, along with self-hosted systems, using a mix of Cloud and typically Microservice Based self-hosted integrations to achieve complex integrations spanning multi-cloud SaaS and self-hosted end points.
