# 4.2 Workflow/FlowServices Capability Comparison

| Item                            | Worflow                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | FlowService                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| ------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| UX                              | Graphical canvas, drag and drop, left to right creation of an automation, linking connectors/actions with arrows, presented in a diagrammatic format.                                                                                                                                                                                                                                                                                                                                                                                                                              | Programmatic creation of an integration service through keyboard or vertically oriented drag and drop, in a top to bottom orientation, presented as programmatic logic.                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Data Mapping                    | [Simple to use data mapper](https://docs.webmethods.io/integration/workflow_building_blocks/creating_first_workflow/), that allows all prior action data to be mapped to the current action as needed, with a visual display of mapping, and outcomes using recorded test data.  Provides a large set of data transformers that can be used to transform data during mapping                                                                                                                                                                                                          | [Complex data mapper](https://docs.webmethods.io/integration/developer_guide/flowservices/#co-pipeline_intro) with a large set of transformers, that facilitates any mapping need, including transformation of data types, enumeration and  structures, as well as index and conditional mapping                                                                                                                                                                                                                                                                                                 |
| Decisional Logic Constructs     | [Switch](https://docs.webmethods.io/integration/additional_features/switch/)&nbsp;                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | [Switch](https://docs.webmethods.io/integration/developer_guide/flowservices/), [if/then/else](https://docs.webmethods.io/integration/developer_guide/flowservices/)                                                                                                                                                                                                                                                                                                                                                                                                                                |
| Looping Constructs              | [Simple Loop (Repeat X times)](https://docs.webmethods.io/integration/additional_features/loop/), [Simple Loop (Repeat over list)](https://docs.webmethods.io/integration/additional_features/loop/)                                                                                                                                                                                                                                                                                                                                                                                    | [Repeat X Times](https://docs.webmethods.io/integration/developer_guide/flowservices/#co-coreelements), [Repeat over list](https://docs.webmethods.io/integration/developer_guide/flowservices/#co-coreelements), [Repeat over list1 and list2](https://docs.webmethods.io/integration/developer_guide/flowservices/#co-coreelements), [While/do](https://docs.webmethods.io/integration/developer_guide/flowservices/#co-coreelements), [do/until](https://docs.webmethods.io/integration/developer_guide/flowservices/#co-coreelements)                                                                    |
| Triggers to start integrations  | [webhook/http](https://docs.webmethods.io/integration/workflow_building_blocks/trigger/), [Schedule](https://docs.webmethods.io/integration/workflow_building_blocks/trigger/), [API](https://docs.webmethods.io/integration/apis/rest_api_builder/), [System triggers](https://docs.webmethods.io/integration/workflow_building_blocks/trigger/)                                                                                                                                                                                                                                            | [http](https://docs.webmethods.io/integration/developer_guide/flowservices/#co-tasksflowservices), [Schedule](https://docs.webmethods.io/integration/developer_guide/flowservices/#co-tasksflowservices), [API](https://docs.webmethods.io/integration/apis/rest_api_builder/), [Listeners](https://docs.webmethods.io/integration/developer_guide/listeners/)                                                                                                                                                                                                                                            |
| Scripting Capabilities          | [Node.js action](https://docs.webmethods.io/integration/developer_guide/creating_custom_actions_with_nodejs/)                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | [is already a scripting language](https://docs.webmethods.io/integration/developer_guide/flowservices/)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| Connector Creation Capabilities | [REST Connector](https://docs.webmethods.io/integration/connectors/connector-bundle/custom-con/#co-rest_connectors), [SOAP Connector](https://docs.webmethods.io/integration/connectors/connector-bundle/custom-con/#co-overview_soap_connector), [webMethods.io Connector Builder](https://tech.forums.softwareag.com/t/webmethods-io-connector-builder/240109), [On-Premise Connectors](https://docs.webmethods.io/integration/connectors/connector-bundle/custom-con/#co-on_premises_connectors), [Node.JS CLI](https://docs.webmethods.io/integration/developer_guide/connector_builder/) | [REST Connector](https://docs.webmethods.io/integration/connectors/connector-bundle/custom-con/#co-rest_connectors), [SOAP Connector](https://docs.webmethods.io/integration/connectors/connector-bundle/custom-con/#co-overview_soap_connector), [webMethods.io Connector Builder](https://tech.forums.softwareag.com/t/webmethods-io-connector-builder/240109), [On-Premise Connectors](https://docs.webmethods.io/integration/connectors/connector-bundle/custom-con/#co-on_premises_connectors), [Flat File](https://docs.webmethods.io/integration/connectors/connector-bundle/custom-con/#co-flatfile) |
| Doctype Support                 | No                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 | [Yes](https://docs.webmethods.io/integration/developer_guide/flowservices/#co-document_types)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| Connector Support               | All Connectors except for:<br />B2B related connectors<br />- Electronic Data Interchange<br />- FlatFile<br />- webMethods.io B2B<br />SAP ERP Connector<br />Connector support documented for each connector [Here](https://docs.webmethods.io/integration/connectors/connector/)                                                                                                                                                                                                                                                                                                   | B2B related connectors<br />All Enterprise Connectors<br />(Some typically non mission ciritcal connectors are not supported)<br />Connector support documented for each connector [Here](https://docs.webmethods.io/integration/connectors/connector/)                                                                                                                                                                                                                                                                                                                                          |