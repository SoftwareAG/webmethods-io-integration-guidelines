# 6 Implementation Patterns

## **6.1 Large File Handling**

It is impossible to state an exact size of a File that a workflow or FlowService can process as this depends on the constructs used within the integrations.  
When handling large files, loading any large file into memory, parsing, converting, etc. is almost always likely to create an 'out of memory' issue no matter what technology is used.  You can witness this yourself simply trying to load a very large file into Microsoft Notepad in Windows, which attempts to load the whole file into memory, unlike something like Notepad++ which only retrieves segments of files you're viewing/working on.

Bearing this in mind, ANY integration which loads a file into memory could cause issues.

So, how do you manage to work with large files?

### **Workflow**

Workflow executes in a 1GB container, which means any large file loaded into memory will likely cause issues, particularly if you pass the file data to other actions, which will create additional copies in memory.  
All workflow actions are additive to the amount of data held in memory in the execution environment.  The more actions you have in a workflow, the more memory becomes consumed as the workflow progresses.

Workflow for the most part can work with large files so long as you do NOT need to transform the data.  If you're moving content of a file from one system to another, this works so long as you utilize connectors that do not load the entire file by working with the item from the file store:

e.g. download a file from Microsoft SharePoint, upload to an SFTP site
![screenshot](../image/development-guidelines/Filepath.PNG)

or you use connectors that along with readable file streams, support streaming the data, rather than loading the whole file into memory at once:
![screenshot](../image/development-guidelines/FileStream.PNG)

This means that you cannot change/transform the file content.

Typically, most file actions work in one of these ways, however if you attempt to use the 'Read File' action, or use any connector which takes the file and returns content into the workflow, this will cause issues with large files or looping constructs.

Such examples that may cause issues with large files are:

* SpreadSheet Reader
* Read File
* ...

If you need to transform a large data file, there are multiple ways to achieve this

1. **Chunk the files at source** - if these are CSV files, repeating JSON nodes or XML nodes, the files can be chunked into smaller parts to avoid loading a complete file into memory.  If these can be chunked at source, they can be more easily parsed/transformed
2. **FlowServices** (see below)
3. If this is big data integration, consider using our **data integration platform [StreamSets](https://streamsets.com/)**

### **FlowServices**

FlowServices have ~14GB of RAM available which sounds a lot, however this can also be quickly consumed with large files.
Consider an XML file, or a JSON file.  If this XML file has 1GB of data in it, and you want to put this into an XML DOM structure in memory, the memory consumption on this would be huge, easily more than 10 times the File size, which can quickly exhaust the available memory.

Working with FlowServices is no different.  If you create DocTypes/Document structures, and try to populate this with a large data set, this can quickly consume the memory on the environments, therefore alternate approaches need to be considered to parse and transform large files, including CSVs and/or fixed format files.

**Working with Large CSVs/Fixed Format Files** - this is the most common and typical integration use case, quite often related to B2B implementations using EDI/CSV, etc.  
webMethods.io Integration has a connector that is only available to the FlowService engine called [FlatFile](https://docs.webmethods.io/integration/connectors/connector-bundle/custom-con/#co-flatfile).  This connector allows you to define a structure of a file, either separated, or fixed length, and then you can use this created connector to parse a data file.

By default, this will still attempt to load the FlatFile document into memory and convert this to a doctype - however for large documents, this will create memory issues, and therefore you should use the 'ffIterator'

![screenshot](../image/development-guidelines/FFIterator.PNG)

When using ffIterator, rather than loading the file in memory, you can define your FlowService logic to iterate through each record one by one allowing you to transform and process each record individually however you choose.

Processing each line can be done in a called FlowService (to make editing easier), or can even be done through a messaging publish with a FlowService subscriber (or even a workflow).
Using the FlatFile (FF) Connector with ffIterator allows you to read and process ANY file size, where you can fully configure delimiters, etc. for any needs.


## **6.2 Using FlowServices & Workflows Together**

Transporting large data between workflows and FlowServices may also cause problems with the Workflow Engine, therefore if you do need to transport large data between them, there are a few implementation patterns you can use to do this

1. **Use Messaging** - This option really depends on the file size.  Once you've downloaded and read the file, you can send the file data via a messaging call to a FlowService by publishing the content, then subscribe from a FlowService to process the whole message.  As a FlowService has more memory, it's easier to chunk/split and parse sections of the file.  In addition, you can use a topic and have multiple processors of the data via messaging.
2. **Use an Intermediary Store (e.g. AWS S3) -** Have a workflow trigger move a large file to an intermediary file store, e.g. download a file from Microsoft SharePoint and move to an AWS S3 location.  Once moved, you can pass the S3 location to a FlowService via a call, or via messaging if you're doing multiple files. Please use queues and serialized subscribers if order is important.

## **6.3 Workflow - Transforming data**

You can use a combination of a [JSON Customizer](https://docs.webmethods.io/integration/additional_features/json_customizer/#gsc.tab=0) as well as transformers to make some significant changes to the data structures in a workflow, however you might find it easier to create a FlowService.

## **6.4 Workflow - Parallel Processing**

Workflows do not have to be sequential - they can have parallel execution threads allowing more than one action to run concurrently.  Be cautious using these and remain conscious of error handling in these scenarios.
