---
description: >-
  This guide will demonstrate how to delete old reports and screenshots from
  TestProject platform to free storage quota or for housekeeping purposes
---

# Deleting old reports

## Deleting Reports Manually from TestProject UI

1. Navigate to the reports page

![](../.gitbook/assets/image%20%28221%29.png)

2.  Select which Project to view the reports from, by default it will select the current Project

![](../.gitbook/assets/image%20%28220%29.png)

3. You can select the time range to filter the date of the reports, by default it will select the last 30 days.

![](../.gitbook/assets/image%20%28192%29.png)

4. You can see all the Job and single Test executions in the given time range, select the Job you wish to delete the reports from



![](../.gitbook/assets/image%20%28156%29.png)

5. You can then press on which tests to delete, or Select All, then press on Delete

![](../.gitbook/assets/image%20%28171%29.png)



## Deleting Reports by Using The Restful API \(Bulk Delete\)

1. Get or Generate your API key here: [https://app.testproject.io/\#/integrations/api](https://app.testproject.io/#/integrations/api)

![](../.gitbook/assets/image%20%28126%29.png)

2. Copy the API key.

3. Navigate to the API Swagger here: [https://api.testproject.io/docs/v2/\#/](../testproject-addons/available-addons/ios-wheel-picker.md)

4. Authorize your account by clicking on the Authorize button and pasting the API key.

![](../.gitbook/assets/image%20%28135%29.png)

![](../.gitbook/assets/image%20%28223%29.png)



5. Scroll down to Reports or click here: 

[https://api.testproject.io/docs/v2/\#/](https://api.testproject.io/docs/v2/#/)

We have many options to choose on how to delete reports.

### Delete all Project and Test Reports

Using this Endpoint [https://api.testproject.io/docs/v2/\#/Reports/Reports\_DeleteProjectReportsAsync](https://api.testproject.io/docs/v2/#/Reports/Reports_DeleteProjectReportsAsync)

We can delete all the project reports or pick a specific start and end date.

**First, we need to get the Project ID**:

In your projects page:

![](../.gitbook/assets/image%20%28147%29.png)

Click on the 3 dots near the Project name:



![](../.gitbook/assets/image%20%28222%29.png)

Select COPY ID:

![](../.gitbook/assets/image%20%28178%29.png)



Back in the API Swagger page, paste the Project ID:

![](../.gitbook/assets/image%20%28107%29.png)

In the **deleteParameters** field, we can decide on which reports we want to delete.

* **From** - The date from where to begin deleting reports.
* **To** - The date from until to delete the reports.
* **OlderThan** - Delete all reports until that date.

To delete all Project reports, just delete "**from**" and "**to**", it will automaticlly generate the current date in the "**olderThan**" field.

![](../.gitbook/assets/image%20%2872%29.png)



Execute the request:

![](../.gitbook/assets/image%20%28130%29.png)

Once it is done, you will see the "200" response, and the reports will be deleted.

![](../.gitbook/assets/image%20%2889%29.png)

`In case you are getting 401, make sure you are authorized as seen previously.`



