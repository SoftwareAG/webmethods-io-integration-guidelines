# 5.1 Workflows

## **5.1.1 When to use Workflows**

* Event based integrations  "when *something* happens in System A, then do *something* in System B"
* If your need is for longer running __asynchronous__ integrations (up to 30 minutes)
* If you aim is for simple asynchronous __low throughput__ orchestration of __2 or 3 connectors__ and FlowServices together with __minimal transformation__ needs
* When you want to use a connector currently not available in the FlowServices IDE
* When you want to trigger an automation from a system connector

## **5.1.2 When NOT to use Workflows**

* If you have more than 15 to 20 actions in a workflow
* If you're using lots of HTTP calls
* You're only orchestrating flow services
* If you're trying to write complex programmatic logic using workflow orchestration
* If you're using lots of store actions to programmatically adjust data
* When you have complex mapping needs
* When you have more than one, or complex loops
* If you expect realtime synchronous responses
* If you have a high throughput, high performance requirement
* If you're dealing with large volumes of data
* If you're exposing this as a real-time synchronous API
* If you're implementing integrations for B2B

## 5.1.3 Workflow Do's and Don'ts

* **Don't** create nested loops, or have more than 1 or 2 loops.  This will quickly result in memory issues
* **Don't** write extremely complex Node.JS actions - better to put this into a CLI connector.
* **Don't** loop through a list to find a specific value, rather use JSON Path action
* **Don't** abuse the store actions.  These are for very simple storage, not large or complex items that need ot be queried
* **Do** remember that transformers can work with lists, dates, etc.
* **Do** use other SaaS services, e.g. Azure DB / Amazon RDS for you own data storage needs
* **Do** remember that a workflow commits a messaging item off a queue as soon as the trigger is complete, meaning you must handle this condition if something fails, or stick to FlowServices for messaging.
* **Do** take care with email actions, there's more than one choice and each offers different capability, including SMTP, Send an Email, Office 365.
* **Do** try to use the accounts feature for secure storage of secrets where possible for username/passwords/keys/etc, rather than defaulting these in mapping statements. It's better to create a REST connector than use HTTP or Swagger/RAML actions for this reason.
