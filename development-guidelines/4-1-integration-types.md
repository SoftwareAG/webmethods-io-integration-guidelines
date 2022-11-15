# 4.1 Integration/Automation Types

webMethods.io Integration currently provides two different approaches for developing integrations

* No-code Workflow Automations
* Low-code FlowSerivces Integrations

First, I'd like to explain the differences between these two approaches, their target persona, and some of the characterstics between these.

## 4.1.1 Workflow

### Overview

[Workflow](https://docs.webmethods.io/integration/workflow_building_blocks/creating_first_workflow/) is a __No-code__ graphical orchestration editor, facilitating the creation of automations for a non-devloper.  A user constructs workflow automations by dragging and dropping actions and integration blocks (typically created by more technical users), then links these with simple decisional logic by dragging arrows between the actions, and same with the data fields.

Workflow is intended to be powerful, yet very easy to way to orchestrate pre-existing assets including the out-of-the-box connectors, and as such the lacks complex conditional logic and looping constructs a typical developer or integration specialist user would expect.

Due to it's power, some people mistake workflow for a programmatic construction tool, and can often attempt to create very complex logic which is a misuse of the tool.

### Typical Users/Persona

Workflow is most typically used by a __Technical business user__.

Somebody usually from the business side of the organziation (not IT), and uses technology for business usage, with both internal and external needs.  They tend to have good IT experience, and can understand basic programmatic logic and constructs, and as such are more than capable of using no-code applciations.  Some of these people maybe more technical roles such as data scientist, software engineers and even developers, but are still part of a non-technical team, e.g. Marketing and often responsible for algorthims, analytics, pricing, and integration of data flows, and/or customer service interactions.

In additon to being used primarliy by the technical business user, workflows are also used by more developer centric roles because of the simplicity, allowing them to focus on the business need, and avoid the congitive load of creating a more complex solution.

## 4.1.2 FlowServices

### Overview

[FlowServices](https://docs.webmethods.io/integration/developer_guide/flowservices/) are __Low-Code__ integrations, providing more programmatical constructs for power users, and those comfortable with programming, such as if/then/else, try catch, and complex looping such as repeat, do/until, and while do statements.  FlowService enforce an input and output contract, ensuring you think about the data that it will receive and return, and along with this facilitates more complex mapping requirements, with conditional maps, index based maps, constructs to rearrange the data structures wholly, and more.

Flows services are created top to bottom, using the keyboard or mouse and represented like a typical program, howevever the powerful mapper is used in place of variable definitions and data logic.

They are also the exact same FlowSerivces that existing in our self-hosted products, so a user with existing knowledge of webMethods can quickly and easily pick up and create FlowService logic in minutes.

### Typical Users/Persona

FlowServices are typically used by __Integration Specialists / Developers__.

An integration specialist provides integration expertise, and often work in an Integration Center or Excellence (or competency center), responsible for integration of 'Tier 1' systems of records that are mission critical, and often on-premise, though more frequently includes the large SaaS vendors now.  Since they work with tier 1 systems, they need to implement complex logic that is fault tolerant, and implement high throughput, high performance real time integrations. Developers have a similar skill set but come from a more standard programmatic background and as such look for recognizable programmatic constructs.
