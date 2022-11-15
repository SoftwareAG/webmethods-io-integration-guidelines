# 9 Connector Development {9}

## 9.1 REST Connectors {9.1}

If you need to call a REST based system but there's no connector available, there are a few choices to implement this

### 9.1.1 HTTP Action in workflow {9.1.1}

This is not recommended to be used other than for quick tests/proof points.  Any secrets/etc have to be provided in the mapping, which makes this less secure.  If you do use this, please use the project parameters marking items as passwords were needed.  In addition, this action is only useful in this particular workflow so inhibits any reuse of the connector.

## 9.1.2 Swagger/RAML actions in workflow {9.1.2}

Like HTTP actions, this is also not recommened as has the same issues as the HTTP action.

## 9.1.3 REST Connector Creator {9.1.3}

The [REST connector creator](https://docs.webmethods.io/integration/connectors/connector-bundle/custom-con/) provides the facility to manually create a reusable connector scoped to the project that makes use of the account functionality to store secrets, as well as managing multiple auth types, headers, and much more.  This makes this a great choice for less technical people to create a REST connector in the UX.  Currently this does not support creation via an API specification.

#### 9.1.4 Connector Builder - Node.JS CLI {9.1.4}

The [Node.JS CLI](https://docs.webmethods.io/integration/developer_guide/connector_builder/) allows a JavaScript developer to quickly create a connection from scratch, from an OpenAPI specification, or even from a Postman collection, as well as implementing any auth scheme required.  These connectors can be installed into any tenant and deployed from one tenant to another.

Please note, you can override a connector version, however if you change the connector interface, you will need to re-link/map this into the workflow again.  As such you can deploy the connector at the same version it you've not change the interface or only added new functions, however you should increment the version is you do change the interface.

Also note, that Node.JS CLI connectors can only be used in the Workflow currenly.

## **9.1.5 Connector Builder - Cloudstreams** {9.1.5}

The [webMethods.io Connector Builder](https://tech.forums.softwareag.com/t/webmethods-io-connector-builder/240109) can be used to programmatically create REST connectors using Software AG's FlowServices and/or Java using multiple authentication options, with complex knowledge.  These can also be created from REST Specifications (e.g. openapi).

Cloudstreams based connectors can be used both in Flow and Workflow, however stream types are only supported within a FlowService.

## 9.2 SOAP Connector {9.2}

Like REST connectors, SOAP connectors can be created both in the UX, and via  the webMethods.io Connector Builder through Cloudstreams

## 9.3 Database Connector {9.3}

The database connector allows you to utilize databases for queries/stored procedure calls, and modifications to table data.  This is a power function available to both Workflow and FlowServices, however please remember that

1. By default, transactions are implicitly managed, however, self managed transasctionality is available in a FlowService.
2. Your database needs to be accessible from Software AG's cloud environment.  Please proceed with caution if you do this to ensure your database is not open to unauthorized users.
3. As you'll be routing to your database from the cloud, please try to utilize the database correctly.  Do not make multiple calls and service logic if a SQL query can encompass all this.

## 9.4 FlatFile Connector {9.4}

1. This can be utlized either by creating a flat file defition, or directly from within a FlowService without a defintion being created.
2. Large files (>250MB) will cause issues and will need to use the iterator to be processed
3. FlatFile Connector can only be used in a FlowService

## 9.5 OData Connector

OData based systems can be utilized via the generic OData connector

## 9.6 Messaging/JMS Connector

The messaging connector also allows for connection to external JMS based messaging providers.  Currently this only supports Universal Messaging running inside webMethods.io Cloud Container, however this will be expanded moving forward to support self-hosted UM installations as well as other JMS providers Software AG have certified.
