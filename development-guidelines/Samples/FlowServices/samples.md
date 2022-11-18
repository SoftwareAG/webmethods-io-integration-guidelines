# Flow Service Samples

## dateValidation

**Download:** [Here](./dateValidation.zip)

**Description**

This performs a Three stage date validation to ensure a date of birth is valid.

1. First it confirms whether the provided date in yyyy-MM-dd format is valid, for example:| **Valid** | **Invalid**                  |
   | --------------- | ---------------------------------- |
   | 2020-10-19      | 20th March 2020*(Invalid format)*  |
   | 2020-02-29      | 2019-02-31*(28 days in Feb 2019))* |
   | 2020-01-01      | 2020-1-1*(invalid format)*         |
2. Second, if the format is valid, it checks that the date is not in the future (e.g. you might be checking a date of birth).  So 2023-01-01 would be invalid, as would tomorrows date.
3. Third, if the format is valid, and it's not in the future, it finally checks that the date is not more than 150 previous (e.g. in the scenario where you might be checking a date of birth), e.g. 1776-07-04 would be invalid.

**Input**

| **Type** | **Name** | **Description**                                              | **Example** |
| -------------- | -------------- | ------------------------------------------------------------------ | ----------------- |
| str            | dateString     | String containing the year month and day in the format: yyyy-MM-dd | 2019-02-28        |

**Output**

| **Type** | **Name** | **Description**                                                                          | **Example** |
| -------------- | -------------- | ---------------------------------------------------------------------------------------------- | ----------------- |
| str            | valid          | String indicating validity of date.  Where date validation is an issue an error will be throw. | true              |

**Errors**

If the date format isn't valid, a number of different errors can be thrown from the FlowService

1. Date Format Incorrect
   *Either the format has not been supplied as yyyy-MM-dd, e.g. 2020-4-12 or an invalid date was provided, such as 2020-04-53*
2. Date is in the future
   *The date specified is in the future*
3. Date out of Range
   The date specified is more than 150 years ago

---

## Format UK Telephone Number

**Download:** [Here](./formatUkTelephoneNumber.zip)

**Description**

Provides a standardized output of a UK Telephone number, regardless of what format the number was provided in.  For example, if I provide a telephone (mobile/cell) number as 07123 456789 this should be output in a consistent manner, as

+{country code} (0){dialcode}  {number}, i.e. +44 (0)7123 456789.  This also works if I provide a number as +447123456789, etc.

**Input**

| **Type** | **Name** | **Description** | **Example**                           |
| -------------- | -------------- | --------------------- | ------------------------------------------- |
| inPhoneNumber  | dateString     | Telephone number      | 07123 456789, 01332 611000, +44 1332 611000 |

**Output**

| **Type** | **Name** | **Description**                | **Example** |
| -------------- | -------------- | ------------------------------------ | ----------------- |
| str            | countrycode    | Country code                         | 44, 1             |
| str            | dialcode       | Dial code                            | 1332, 7123        |
| str            | number         | 6 Digit UK telephone number          | 456789            |
| str            | formatted      | Formatted output of telephone number | +44 7123 456789   |

---

## xmlString2jsonString.zip

**Download:** [Here](./xmlString2jsonString.zip)

**Description**

Converts a string containing XML to a JSON String preserving array markers ( '[' and ']' ) in the JSON where specified.

**Input**

| **Type** | **Name** | **Description**                                       | **Example**                                                                       |
| -------------- | -------------- | ----------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| str            | xmlString      | String of XML                                               | `<top><list1><item>1</item></list1><list2><test>a</test><test>b</test></list2></top>` |
| str[]          | arrayElements  | textual data to insert or update to the provided identified | [0] ="item"[1] = "test"                                                                 |

**Output**

| **Type** | **Name** | **Description**                    | **Example**                                           |
| -------------- | -------------- | ---------------------------------------- | ----------------------------------------------------------- |
| str            | jsonString     | JSON String converted from the XML input | {"top":{"list1":{"item":["1"]},"list2":{"test":["a","b"]}}} |

---

## XMLStringtoWorkflowStructure.zip

**Download:** [Here](./XMLStringToWorkflowStructure.zip)

**Description**

Converts an XML string to a document structure that can be subsequently used in mapping in FlowService or Workflow.

**Input**

| **Type** | **Name** | **Description**                                       | **Example**                                                                                                            |
| -------------- | -------------- | ----------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| str            | xmlString      | String of XML                                               | `<top><list1>`  `<item>`1 `</item></list1>``<list2>`  `<test>`a `</test>`  `<test>`b `</test></list2>``</top>` |
| str[]          | arrayElements  | textual data to insert or update to the provided identified | [0] ="item"[1] = "test"                                                                                                      |

**Output**

| **Type** | **Name** | **Description**               | **Example**                                                        |
| -------------- | -------------- | ----------------------------------- | ------------------------------------------------------------------------ |
| doc            | response       | document created from XML structure | ![](blob:https://teams.microsoft.com/8665942e-c74f-48d9-82f4-1c3ecd16f1a9) |

---

## htmlContentStream

**Download:** [Here](./htmlContentStream.zip)

**Description**

Service that receives HTML content coming from a REST API post/put.

**Input**

| **Type** | **Name** | **Description**                     | **Example** |
| -------------- | -------------- | ----------------------------------------- | ----------------- |
| obj            | contentStream  | Stream object containing the HTML payload | n/a               |

**Output**

| **Type** | **Name** | **Description**                 | **Example**         |
| -------------- | -------------- | ------------------------------------- | ------------------------- |
| str            | output         | String that contains the HTML payload | `<HTML>`....`</HTML>` |

## Large FlatFile CSV Processing

---

**Download:** [Here](./FlatFile_Processing.zip)

**Description**

Downloads a large CSV file from a URL, and iterates and parses through this using the FlatFile connector.

Contains a 'time limit' to ensure that the integration can be stopped after a specific time if required, which is hard coded on the first step

Please note also - tenants have a global timeout for While/do/until/repeat - default typically 6 hours.

---

## Date/Time to Epoch

**Download:** [Here](./dateTimeToEpoch.zip)

**Description:**

Converts a date time to epoch (millis) time

**Input**

| **Type** | **Name** | **Description**  | **Example** |
| -------------- | -------------- | ---------------------- | ----------------- |
| String         | year           | Year (4 digits)        | 2022              |
| String         | month          | Month (2 digits)       | 09                |
| String         | day            | Day (2 digits)         | 05                |
| String         | hour           | Hour (24h / 2 digits)  | 11                |
| String         | min            | Min (2 digits)         | 25                |
| String         | sec            | Sec (2 digits)         | 00                |
| String         | millis         | millseconds (3 digits) | 000               |

**Output**

| **Type** | **Name** | **Description** | **Example** |
| -------------- | -------------- | --------------------- | ----------------- |
| String         | epochDateTime  | epochTime             | 1652095500000     |

---

## Epoch DateTiime to Excel

**Download:** [Here](./convertEpochDateToExcel.zip)

**Description:**

Converts an epoch time (millis) to an excel date value

**Input**

| **Type** | **Name** | **Description**  | **Example** |
| -------------- | -------------- | ---------------------- | ----------------- |
| String         | epoch          | epochDateTime (millis) | 1652095500000     |

**Output**

| **Type** | **Name** | **Description** | **Example** |
| -------------- | -------------- | --------------------- | ----------------- |
| String         | excel          | excel date value      | 44690.47569       |

---

## Timer

---

**Download:**
[startTimer](./startTimer.zip)
[stopTimer](./stopTimer.zip)

**Description**

Provides in FlowService nanosecond based timer for timing usages where required to help with long executions, etc.  This is provided by two flow services.  startTimer and StopTimer.
This uses 

### **Start Timer**

**Input**

| **Type** | **Name** | **Description** | **Example** |
| -------------- | -------------- | --------------------- | ----------------- |
| n/a            |                |                       |                   |

**Output**

| **Type** | **Name** | **Description**                    | **Example** |
| -------------- | -------------- | ---------------------------------------- | ----------------- |
| Long           | startTime      | nanosecond time value when timer started | 3743784331581797  |

### **Stop Timer**

**Input**

| **Type** | **Name** | **Description**                                                | **Example** |
| -------------- | -------------- | -------------------------------------------------------------------- | ----------------- |
| startTime      | Long           | Output from the startTimer service (nanosecond timer)                | 3743784331581797  |
| timerName      | String         | Descriptive name to attribute to the time for output                 | myTimer           |
| doNotLog       | String         | If exists, will not log to LogCustomMessage (visible in monitoring) | false             |

**Output**

| **Type** | **Name** | **Description**                    | **Example** |
| -------------- | -------------- | ---------------------------------------- | ----------------- |
| Long           | startTime      | nanosecond time value when timer started | 3743784331581797  |
