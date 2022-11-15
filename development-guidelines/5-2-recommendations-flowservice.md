# 5.2 FlowServices

## 5.2.1 When to use FlowServices

* If your need is for __synchronous__ integrations
* If you need high throughput, realtime and high performing integrations
* If you have complex programmatic logic/decisional conditions
* When your system has no standard APIs
* You have complex mapping requirements
* Need for many loops, nested, and/or different types
* If you need to restructure the data, types, formats, etc
* If you are processing large files or responses from systems
* If you're working with B2B and need to parse/validate and consume/transform EDI and other B2B payloads
* If you need to parse and transform otehr large 'flat-files', e.g, CSV, Fixed File format.
* If you're combining SOAP APIs for real time data exposure
* If you're combining REST APIs for real time data exposure
* Need complex exception handling and retry logic

## 5.2.2 When NOT to use FlowServices

* When you don't have programmatic skills
* When you are creating something simple
* When you want to create Node.JS basedCLI Connectors/actions

## 5.2.3 FlowService Do's and Don'ts

* **Don't** invoke another FlowService to try and reuse integrations via HTTP - this results in significant overhead as you'll be routing out and into the platform again.  Instead think about integrations as Microservices, with replication rather than reuse, resulting in simpler and self contained deployments versus more complex dependency managed deployments that typically occur with an SOA style implementation.
* **Don't** over use the LogCustomMessage service - this adds input/output database overhead to your invocations and will result in slower performance - only use this for small amounts of data, and in exceptional scenarios
* **Don't** use For loop with a counter, rather use loop over a list, while/do do/until.  For loop with a counter currently has a significant performance penalty with a 1 second delay between each iteration
* **Don't** attempt to create/mimic stateful services through the use of storage services/etc.
* **Do** specify your service contract using constraints so you can easily validate the inputs/outputs.
* **Do** keep the pipeline clean as you go - this not only makes mapping simpler as there's much less to select, but also helps to keep the memory clean.
* **Do** consider error cases in particular on top-level FlowServices.  What happens if you try/catch, how do you signify to the platform/audit that a FlowService has failed, or a workflow thats invoked the FlowService.
* **Do** make sure your pipeline at the last step matches the output - specifically take note of arrays/document lists.  If you're returning a list with a single item, this should still be a list and not a single item, and could cause other issues with subsequent steps/calls.
* **Do** make sure and while/do do/until loop has a condition to exit that will fire.  Without this the FlowService will run for 6 hours before it times out (which equals 7200 transactions).  You can use CurrentNanoTime to make a time restricted while/do do/until loop if required to catch any accidental runs over a certain time period
* **Do** remember FlowServices can be recursive for complex requirements, but take care not to create a stack overflow error.
