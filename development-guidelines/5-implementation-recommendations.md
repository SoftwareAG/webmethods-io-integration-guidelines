# 5 Implementation Recommendations

## 5.1 Workflows

### **5.1.1 When to use Workflows**

* Event based integrations "when *something* happens in System A, then do *something* in System B"
* If your need is for longer running __asynchronous__ integrations (up to 30 minutes)
* If your aim is for simple asynchronous __low throughput__ orchestration of __2 or 3 connectors__ and FlowServices together with __minimal transformation__ needs
* When you want to use a connector currently not available in the FlowServices IDE
* When you want to trigger an automation from a system connector

### **5.1.2 When NOT to use Workflows**

* If you have more than 15 to 20 actions in a workflow
* If you're using lots of HTTP calls
* You're only orchestrating flow services
* If you're trying to write complex programmatic logic using workflow orchestration
* If you're using lots of store actions to programmatically adjust data
* When you have complex mapping needs
* When you have more than one loop, or complex loops
* If you expect real-time synchronous responses
* If you have a high throughput, high performance requirement
* If you're dealing with large volumes of data
* If you're exposing this as a real-time **synchronous** API
* If you're implementing integrations for B2B

### 5.1.3 Workflow Do's and Don'ts

* **Don't** create nested loops, or have more than 1 or 2 loops.  This will quickly result in memory issues
* **Don't** write extremely complex Node.JS actions - better to put this into a CLI connector.
* **Don't** loop through a list to find a specific value, rather use JSON Path action
* **Don't** abuse the store actions.  These are for very simple storage, not large or complex items that need to be queried
* **Do** remember that transformers can work with lists, dates, etc.
* **Do** use other SaaS services, e.g. Azure DB / Amazon RDS for you own data storage needs
* **Do** remember that a workflow commits a messaging item off a queue as soon as the trigger is complete, meaning you must handle this condition if something fails, or stick to FlowServices for messaging.
* **Do** take care with email actions, there's more than one choice and each offers different capability, including SMTP, Send an Email, Office 365.
* **Do** try to use the accounts feature for secure storage of secrets where possible for username/passwords/keys/etc, rather than defaulting these in mapping statements. It's better to create a REST connector than use HTTP or Swagger/RAML actions for this reason.

## 5.2 FlowServices

### 5.2.1 When to use FlowServices

* If your need is for __synchronous__ integrations
* If you need high throughput, real-time and high performing integrations
* If you have complex programmatic logic/decisional conditions
* When your system has no standard APIs
* You have complex mapping requirements
* Need for many loops, nested, and/or different types
* If you need to restructure the data, types, formats, etc.
* If you are processing large files or responses from systems
* If you're working with B2B and need to parse/validate and consume/transform EDI and other B2B payloads
* If you need to parse and transform other large 'flat-files', e.g, CSV, Fixed File format.
* If you're combining SOAP APIs for real time data exposure
* If you're combining REST APIs for real time data exposure
* If you need complex exception handling and retry logic

### 5.2.2 When NOT to use FlowServices

* When you don't have programmatic skills
* When you are creating something simple
* When you want to create Node.JS based CLI Connectors/actions

### 5.2.3 FlowService Do's and Don'ts

* **Don't** invoke another FlowService to try and reuse integrations via HTTP - this results in significant overhead as you'll be routing out and into the platform again.  Instead, think about integrations as Microservices, with replication rather than reuse, resulting in simpler and self-contained deployments versus more complex dependency managed deployments that typically occur with an SOA style implementation.
* **Don't** over use the LogCustomMessage service - this adds input/output database overhead to your invocations and will result in slower performance - only use this for small amounts of data, and in exceptional scenarios
* **Don't** use For loop with a counter, rather use loop over a list, while/do do/until.  For loop with a counter currently has a significant performance penalty with a 1 second delay between each iteration
* **Don't** attempt to create/mimic stateful services through the use of storage services/etc.
* **Do** specify your service contract using constraints so that you can easily validate the inputs/outputs.
* **Do** keep the pipeline clean as you go - this not only makes mapping simpler as there's much less to select, but also helps to keep the memory clean.
* **Do** consider error cases in particular on top-level FlowServices.  What happens if you try/catch, how do you signify to the platform/audit that a FlowService has failed, or a workflow that has invoked the FlowService.
* **Do** make sure your pipeline at the last step matches the output - specifically take note of arrays/document lists.  If you're returning a list with a single item, this should still be a list and not a single item, and could cause other issues with subsequent steps/calls.
* **Do** if you use while/do or do/until loops, make sure they have a condition to exit that will fire.  Without this the FlowService will run for 6 hours before it times out (which equals 7200 transactions!).  You can use CurrentNanoTime to make a time restricted loop, if required, to catch any accidental runs over a certain time period
* **Do** remember FlowServices can be recursive for complex requirements, but take care not to create a stack overflow error.

### 5.2.4 FlowService Samples

See [Here](/development-guidelines/Samples/FlowServices/samples.md/) for some FlowService Samples
