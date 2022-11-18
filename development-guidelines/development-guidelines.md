# 1 Introduction

This whitepaper provides information and guidelines for a webMethods.io integration developer, explaining the approaches, benefits and drawbacks on each approach, and provides some guidelines and recommendations as to which approach to pick and when, based on the functionality, and the skills of the person developing the integrations to integration applications.

This white paper focuses on the EiPaaS and Hybrid styles of application integration using [webMethods.io Integration](https://www.softwareag.com/en_corporate/platform/integration-apis/api-integration-platform.html) providing some recommendations, approaches, patterns, and guidance on what and how to implement using Softare AG's EiPaaS.

# 2 Contents

| #     | Page                                                                                                | Description                                                                                           |
| ----- | --------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| 1.    | [Introduction](#1-introduction)                                                                        |                                                                                                       |
| 2.    | [Contents](#2-contents)                                                                                |                                                                                                       |
| 3.    | [What is Application Integration?](3-what-is-application-integration.md)        | Overview of application integration, what this is, approaches, and stylers                            |
| 4.    | [Developer Guidelines](4-developer-guidelines.md)                               | Developer Guidelines for webMethods.io Integration                                                    |
| 4.1   | [Integration/Automation Types Overview](4-developer-guidelines.md)              | Explanation of the different types of integration and automation possible in webMethods.io Itegration |
| 4.2   | [Workflow/FlowServices Capability Comparison](4-developer-guidelines.md)        | Compares functionality of Workflows vs FlowServices                                                   |
| 4.3   | [Workflow/FlowServices Performance Characteristics](4-developer-guidelines.md)  | Compares the performance characteristics of Workflows vs FlowServices                                 |
| 5.    | [Implementation Recommendations](5-implementation-recommendations.md)           | Provides recommendations for implementing integrations                                                |
| 5.1   | [Workflows](5-implementation-recommendations.md)                                | Recommendations for Workflows                                                                         |
| 5.1.1 | [When to use Workflows](5-implementation-recommendations.md)                    | Explains when you should consider use of workflows                                                    |
| 5.1.2 | [When NOT to use Workflows](5-implementation-recommendations.md)                | Explains when you should NOT use workflows                                                            |
| 5.1.3 | [Workflow Do&#39;s and Dont&#39;s](5-implementation-recommendations.md)         | Documents the Do's and Don'ts of workflows                                                            |
| 5.2   | [FlowServices](5-implementation-recommendations.md)                             | Recommendations for FlowServices                                                                      |
| 5.2.1 | [When to use FlowServices](5-implementation-recommendations.md)                 | Explains when you should consider using FlowServices                                                  |
| 5.2.2 | [When NOT to use FlowServices](5-implementation-recommendations.md)             | Explains when you should NOT use FlowServices                                                         |
| 5.2.3 | [FlowService Do&#39;s and Don&#39;ts](5-implementation-recommendations.md)      | Documents the Do's and Don'ts of FlowServices                                                         |
| 5.2.4 | [FlowService Samples](5-implementation-recommendations.md)      | Sample FlowServices providing some different functions                                                         |
| 6.    | [Implementation Patterns](6-implementation-patterns.md#6)                       | Provides some implementation patterns                                                                 |
| 6.1   | [Large File Handling](6-implementation-patterns.md#6.1)                         | Describes problems and solutions to work with large files                                             |
| 6.2   | [Using FlowServices &amp; Workflows Together](6-implementation-patterns.md#6.2) | Describes some approaches to use FlowServices & workflows together                                    |
| 6.3   | [Workflow - Transforming data](6-implementation-patterns.md#6.3)                | Explains how to transform data in workflows                                                           |
| 6.4   | [Workflow - Parallel Processing](6-implementation-patterns.md#6.4)              | Explains workflow parallel processing                                                                 |
| 7.    | [API-Led Integration](7-API-led-integration.md#7)                               | How to implement API-Led Integratoin                                                                  |
| 7.1   | [Implementation (Integration) first API](7-API-led-integration.md#7.1)          | Implementation of an Integration first API                                                            |
| 7.1.1 | [REST API](7-API-led-integration.md#7.1.1)                                      | Implementing REST APIs guidance                                                                       |
| 7.1.2 | [SOAP API](7-API-led-integration.md#7.1.2)                                      | Implementing SOAP APIs guidance                                                                       |
| 7.2   | [API First (REST Descriptor) Implementation](7-API-led-integration.md#7.2)      | Providing an Implementation starting with an API specification                                        |
| 7.3   | [Securing APIs](7-API-led-integration.md#7.3)                                   | Recommendations to secure APIs                                                                        |
| 8.    | [Hybrid Integration](8-hybrid-integration.md)                                   | Hybrid integration implementation information                                                         |
| 9.    | [Connector Development](9-connector-development.md)                             | Describes different approaches to connector development                                               |
| 9.1   | [REST Connectors](9-connector-development.md#9.1)                               | Explains various optoins to invoke a REST based system                                                |
| 9.2   | [SOAP Connector](9-connector-development.md#9.2)                                | In UX configuration to invoke a SOAP based system                                                     |
| 9.3   | [Database Connector](9-connector-development.md#9.3)                            | In UX configuration to invoke database management systems                                             |
| 9.4   | [FlatFile Connector](9-connector-development.md#9.4)                            | In UX configuration to parse fixed/delimited flat files                                               |
| 9.5   | [OData Connector](9-connector-development.md#9.5)                               | In UX configuration to invoke OData APIs                                                              |
| 9.6   | [Messaging/JMS Connector](9-connector-development.md#9.6)                       | in UX configuration to utilize JMS messaging providers                                                |

