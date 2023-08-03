# 9 Connector Development

## 9.1 REST Connectors

If you need to call a REST based system, but there's no connector available, there are a few choices to implement this

| Approach                                                                                                    | Supported in Workflow | Supported in FlowService | Recommendation                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| ----------------------------------------------------------------------------------------------------------- | ---------------------- | ------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| HTTP Action                                                                                                 | Yes                    | Yes                      | These are typically NOT recommended for REST API consumption in production implementations.  Any secrets/etc have to be provided in the mapping, which makes this less secure.  If you do use this, please use the project parameters, and check **Mark as Mandatory** for the parameter.  In addition, this action is only useful in this particular workflow so inhibits any reuse of the connector.                                                                                                                                                                                                                                                                                     |
| Swagger/RAML Actions                                                                                        | Yes                    | No                       | Like HTTP actions, these are also not recommended for REST API consumption in production implementations, for similar reasons at the HTTP Action                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| [REST connector creator](https://docs.webmethods.io/integration/connectors/connector-bundle/custom-con/)       | Yes                    | Yes                      | The REST connector creator provides the facility to manually create a reusable connector scoped to the project that makes use of the account functionality to store secrets, as well as managing multiple auth types, headers, and much more.  This makes this a great choice for less technical people to create a REST connector in the UX.  Currently, this does not support creation via an API specification.                                                                                                                                                                                                                                                                  |
| [Node.JS CLI](https://docs.webmethods.io/integration/developer_guide/connector_builder/)                       | Yes                    | No                       | The REST Node.JS CLI allows a JavaScript developer to quickly create a connection from scratch, from an OpenAPI specification, or even from a Postman collection, as well as implementing any auth scheme required.  These connectors can be installed into any tenant and deployed from one tenant to another.  Please note, you can override a connector version, however if you change the connector interface, you will need to re-link/map this into the workflow again.  As such you can deploy the connector at the same version it you've not changed the interface or only added new functions.
If you do change the interface you should increment the version. |
| [webMethods.io Connector Builder](https://tech.forums.softwareag.com/t/webmethods-io-connector-builder/240109) | Yes                    | Yes                      | The webMethods.io Connector Builder can be used to programmatically create REST connectors using Software AG's FlowServices and/or Java using multiple authentication options, with complex knowledge.  These can also be created from REST Specifications (e.g. OpenAPI).  Please note, stream types are only compatible with FlowServices.                                                                                                                                                                                                                                                                                                                                     |

## 9.2 SOAP Connector

Like REST connectors, SOAP connectors can be created both in the UX, and via the webMethods.io Connector Builder through webMethods CloudStreams

| Approach                                                                                                    | Supported in Workflow | Supported in FlowService | Recommendation                                                                                                                                                                                                                                                                                                                               |
| ----------------------------------------------------------------------------------------------------------- | ---------------------- | ------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| SOAP Connector Creator                                                                                      | Yes                    | Yes                      | The SOAP connector creator provides the facility to manually create a reusable connector scoped to the project that makes use of the account functionality to store secrets.  This makes this a great choice for less technical people to create a SOAP connector in the UX.                                                                 |
| [webMethods.io Connector Builder](https://tech.forums.softwareag.com/t/webmethods-io-connector-builder/240109) | Yes                    | Yes                      | The webMethods.io Connector Builder can be used to programmatically create SOAP connectors using Software AG's FlowServices and/or Java using multiple authentication options, with complex knowledge.  These can also be created from REST Specifications (e.g. OpenAPI).  Please note, stream types are only compatible with FlowServices. |

## 9.3 Database Connector

| Approach           | Supported in Workflow | Supported in FlowService |
| ------------------ | ---------------------- | ------------------------ |
| Database Connector | Yes                    | Yes                      |

The database connector allows you to utilize databases for queries/stored procedure calls, and make modifications to table data.  This is a powerful function available to both Workflows and FlowServices, however please remember that:

1. By default, transactions are implicitly managed, however, self-managed transasctionality is available if using a FlowService.
2. Your database needs to be accessible from Software AG's cloud environment.  Please proceed with caution if you do this to ensure your database is not open to unauthorized users.
3. As you'll be routing to your database from the cloud, please try to utilize the database correctly.  Do not make multiple calls and service logic if a SQL query can encompass all this.
4. Technically it's possible to connect webMethods.io Integration to a database in the self-hosted environment directly, however it is not a recommended architecture. Using the hybrid integration approach is better.

## 9.4 FlatFile Connector

| Approach           | Supported in Workflow | Supported in FlowService |
| ------------------ | ---------------------- | ------------------------ |
| FlatFile Connector | No                     | Yes                      |

1. This can be utilized either by creating a flat file definition, or directly from within a FlowService without a definition being created
2. Large files (>250MB) will cause issues and will need to use the ffIterator to be processed
3. FlatFile Connector can only be used in a FlowService

## 9.5 OData Connector

| Approach        | Supported in Workflow | Supported in FlowService |
| --------------- | ---------------------- | ------------------------ |
| OData Connector | Yes                    | Yes                      |

OData based systems can be accessed via the generic OData connector. Currently, OData v2.0 and 4.0 are supported.

## 9.6 Messaging/JMS Connector

| Approach                                                                                                                                                                                                                                                                                                                                      | Supported in Workflow | Supported in FlowService |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------- | ------------------------ |
| Messaging Connector                                                                                                                                                                                                                                                                                                                           | Yes                    | Yes                      |

 The messaging connector also allows for connection to external JMS based
messaging providers, including using self-hosted UM installations as well as other JMS providers Software AG have certified. Note: The UM Provider within webMethods Cloud Container is supported if needed however do not use this approach if you are not using wM Cloud Container. 
