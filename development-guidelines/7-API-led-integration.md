# 7 API-Led Integration

webMethods.io EiPaaS supports a wide range of integration approaches and patterns, one of which is API-Led Integration, or API-Led Connectivity.  Many organizations start with the integration part of the iPaaS, but over time, might add B2B or API Management to support their needs / digital transformation initiaitves, and an iPaaS lends itself well to this approach as the components are all part of one wider platform.

Many vendors/integrators will tell you that APIs enable access to the systems, but that these should be tiered to foster resuability, akin to an SOA (service oriented architecture) methodology, however this often just serves to create complexity and effort waste with higher development requirements, and ultimatley minimal reuse regardless of the effort.

API-Led Integration rather through an iPaaS is tacked on two fronts

* Connectors, often provided by the platform vendor that utilize APIs and shield the complexities of these from the integrator, to avoid cognitive load and accelerate implementation - these will be covered further down this document.
* The ability to create Integrations from an API specification, or create an API from an Integration - the remainder of this section dicusses and provides guidance around this approach.  This isn't meant to provide an exhaustive guide to create APIs, rather explains the basics and how this can be achieved in webMethods.io Integration.

APIs provided by webMethods.io Integration can be one of two types

* REST - The more modern and now most commonly used type of API
* SOAP - Historically popular, but usage has declined to the point where these are almost non-existant other than in legacy software that hasn't been updated.

## 7.1 Implementation (Integration) first API

### 7.1.1 REST API

A REST API makes use of HTTP verbs to provide data from server resources, typically implemented as follows:

| Verb   | Usage (CRUD)   |
| ------ | -------------- |
| GET    | Read           |
| POST   | Create         |
| PUT    | Update/Replace |
| PATCH  | Update/Modify  |
| DELETE | Delete         |

and use HTTP return codes to signify the state of the response, e.g.

| Return Code | Usage/Description        |
| ----------- | ------------------------ |
| 200/201     | Success                  |
| 204         | No content provided      |
| 404         | Not found/does not exist |
| 405         | Method not allowed       |
| 500         | Internal Error           |

A REST API typically is described via an OpenAPI (Swagger) specification, which can be used by a consumer to understand how to invoke the API, what the resources are, parameters, expected output, and return codes.

As such, this means that the API contract (it's inputs and outputs) must be understood, and potentially even able to be validated for conformity before processing the request.

Workflows in webMethods.io do not have an service contract, therefore to implement an API using a workflow you must

* Use a webhook and define the URL parameters/body which becomes the input
* Use the sync return output and provide a response
* Test both the webhook and the sync return output so the platform can observe the expected inputs/outputs and determine the data from this.

 Once you observe these requirements, you can simply expose the webhook enabled workflow as an API, however this comes with some considerable drawbacks and is therefore __NOT RECOMMENDED__ as an approach for REST APIs.  These drawbacks are:

* There is no explicit typing on the REST API Service contract
* There is no way to validate the inputs
* There could be a wait for a workflow engine to exectute the REST API request

 Therefore if you want to expose APIs from webMethods.io Integration, the __recommended__ mechansim is to create a FlowService and expose this as a REST API.  This recommendation is based no the following:

* A FlowService has defined inputs and outputs that can be both typed and validated with constraints, which generates a well formed and more complete API Specification.
* A FlowService by it's nature is synchronous and executes immediately with no waiting period

 To do this

* Create a Flow Service, providing the input and output parameters, defining any constraints, and types on the service contract
* Implement and test the FlowService, and make sure that the only data that is returned during your test conforms with the Output Parameters, else the response would be invalid compared to the API specification.  To do this use a transform pipeline step in the FlowService, and drop any parameters that are not in the output specification.
* You may alway wish to use try/catch construct to throw appropriate errors should any issues occur during the FlowService implementation
* Avoid the "logCustomMessage" service as this will impact performance of the REST API
* Implement the FlowService in the most efficient way possible.
* Once tested, switch to the [APIs tab](https://docs.webmethods.io/integration/apis/rest_api_builder/#ta-creating_an_api) in the project and press the CreateAPI, then Create from scratch to use the service implementation already created.
* Provide the name version, description and select the content types.
* Add a resource path (e.g. /customer), and select the resource method recalling the HTTP verbs previously, then select the FlowService.

 You API has now been generated and the specification available to download, or via access to the URL.

 Please note:

* The same resource path can be used with different verbs
* An API can have multiple resources if required.
* The accept header can control the format of the API response, e.g. setting accept to Application/XML will cause the API to return the response as XML.  Similar for Application/JSON and text/html.

### 7.1.2 SOAP API

This follows a similar process to the REST API, however due to the tighter requirement for a SOAP service on the input/output specification ONLY FlowServices can be used to provide a SOAP API.

## 7.2 Creation an Integration from an API Specification

You can start an Integration from a REST API Specification - this will take the specification and generate the appropriate FlowServices with service contracts that represent the resources in the REST API.

Once these are generated, you can then proceed to provide the implementation using the FlowService editor.

This option allows you to create an API that conforms to a specification - perhaps your development processes first mean you create an API Specification, alternatively you might want to replace an existing API with an integration, and therefore want to assure that the specification exactly matches to avoid issues with consumers.

## 7.3 Securing APIs.

The APIs (and descriptors) are only accessible by default via HTTP Basic Authentication and requires an iPaaS user credential to be provided that has execute permissions on the the project where the API exists.

It is __NOT RECOMMENDED__ to expose these APIs directly to external consumers as the credential can be used to also login to the iPaaS.  If you must do this, please ensure you create a specific user for this purpose and with access only to execute the integrations in the contained project.

webMethods.io Integration provides alternative mechansims to provide secure APIs through one of:

* [Oauth2](https://docs.webmethods.io/integration/data_access_and_security/oauth20/)
* [Mutual TLS (2-way-ssl)](https://docs.webmethods.io/integration/data_access_and_security/clientcertificate)

Both of these options are available in the settings menu of the iPaaS, however, the best approach is to utilize the [API Gateway and Developer portal](https://docs.webmethods.io/api/index.html#/') to protect, control, and share these APIs with third parties
