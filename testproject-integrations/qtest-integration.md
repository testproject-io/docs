---
description: >-
  Synchronize TestProject test results into qTest for added traceability,
  reporting, and out of the box integration to tools like JIRA.
---

# qTest Integration

## What is qTest?

The **qTest** platform, offered by Tricentis, provides Agile teams with a suite of software testing tools designed to improve speed, efficiency and collaboration throughout the software testing lifecycle.  The platform's flagship product, **qTest Manager** transforms the test case management process, helping enterprise teams get faster and more efficient.  Additionally, **qTest Insights** gives the testing team a self-service business intelligence tool to consolidate, manage and analyze all your test metrics.

## Why do I need qTest Integration?

By integrating **qTest** with TestProject, users will get a number of additional features not included in TestProject, including:&#x20;

* Support for manual testing, with a dedicated repository of manual tests and results in **qTest Manager**
* Out of the box integration and traceability to JIRA, Rally, and VersionOne for defects and requirements management
* Fully customizable reports and dashboards for all test results via **qTest Insights**

## Is qTest included with TestProject?

**qTest** and TestProject are separately licensed and deployed products.  **qTest** is a commercial tool which has a separate license and fee from TestProject.  A [free trial ](https://www.tricentis.com/software-testing-tool-trial-demo/qtest-trial/)of **qTest** is available for 14 days via the Tricentis website.

The **qTest** integration is compatible with any **qTest** Cloud Elite or Cloud Trial licenses.  Future plans are being made to make this feature available to **qTest** On-Premise Elite customers.

## How are qTest and TestProject accounts integrated?

**qTest** users that create a TestProject account from the 9-box will be integrating their **qTest** instance (site) with a newly created TestProject instance.  From that point forward, all newly created TestProject users from that **qTest** instance will be added to the same TestProject instance.

Once an integration is initiated, the **qTest** artifacts that will be integrated with TestProject include:

* **Projects:** new projects will be created in TestProject every time to align with the existing **qTest** project hierarchy.  Users can also create projects directly in TestProject, which will not be integrated back to **qTest**
* **Test Suites:** any new jobs created in TestProject will be synchronized and created as test suites in their corresponding projects in **qTest**
* **Test Runs/Logs:** any new test runs (within a job) created in TestProject will be synchronized to **qTest** as test runs/logs and organized in the proper suites (which relate to TestProject jobs)
* **Test Cases:** for any executed jobs in TestProject, the corresponding test cases will be created in qTest and organized in a separate module named "TestProject".

## Setting up qTest Integration

Users of **qTest** (Cloud Elite or Cloud Trial) should now see the TestProject icon within their 9-box:

![TestProject logo within the qTest 9-box.](<../.gitbook/assets/image (170).png>)

Clicking on the TestProject logo within the **qTest** 9-box will trigger the account creation process in TestProject for that **qTest** user**.**  First, TestProject will check to see if there is an existing TestProject account for that **qTest** user's email address.

If the **qTest** user's email is already established as a user in TestProject, TestProject will skip forward to integrating that TestProject account to the **qTest** account.

If the **qTest** user's email is not yet established as a user in TestProject, TestProject will automatically initiate the process of creating an integrated TestProject account with that user's email address.  First, the user must validate their email address:

![Notification of email validation send to the newly created TestProject user. ](<../.gitbook/assets/image (121).png>)

Then, the user must click the link in the email from TestProject to validate their email address:

![Email validation sent to the user.](<../.gitbook/assets/image (189).png>)

{% hint style="info" %}
If you do not receive the validation email, please contact us at support@testproject.io to manually validate your email.
{% endhint %}

Finally, the user must accept TestProject's separate Terms of Service related to the separate TestProject free license before their account is fully activated and ready to be used:

![TestProject Terms of Service, which must be agreed to for account activation.](<../.gitbook/assets/image (10).png>)

From this point, the integration is automatically set, according to default settings.  You should see the TestProject projects list populated with projects from qTest: &#x20;

![Project list in qTest.](<../.gitbook/assets/image (32).png>)

![Project list in TestProject.  2 projects have been synced from qTest to TestProject.](<../.gitbook/assets/image (134).png>)

{% hint style="info" %}
All projects created in qTest will be synced to TestProject in a 1:1 fashion.  Users should make sure to work in the correct project in TestProject to ensure results from TestProject flow into the proper account in qTest.
{% endhint %}

{% hint style="info" %}
Projects are only synced from qTest to TestProject.  Projects created directly in TestProject will not be created in qTest.
{% endhint %}

## Editing the qTest Integration

The integration between qTest and TestProject will automatically be set and updated each time a user logs in to TestProject from qTest using the 9-box.  If changes need to be made or the integration needs to be turned off completely, you are are able to do so in TestProject in the  Integrations > qTest panel:&#x20;

![Updating the domain, bearer token, or integration status (on/off) from TestProject.](<../.gitbook/assets/image (46) (1).png>)

{% hint style="info" %}
Updating the integration settings incorrectly may result in an interruption in data flow between the two tools.  If you are unsure about making these changes, please contact us at support@testproject.io to assist you before making any updates.
{% endhint %}

## Turning on Automation Settings

To receive data from TestProject into qTest, you must first enable the automation settings in each qTest project by turning the slider to the "ON" status:

![Navigate to the "Automation Settings" area in each project to turn the slider to "ON".](<../.gitbook/assets/image (132).png>)

{% hint style="info" %}
If you decide to edit the mapping of Automation Statuses to qTest Statuses, please make sure you retain a mapping for the "PASS", "FAIL", and "SKIP" status to ensure data is not lost between TestProject and qTest.
{% endhint %}

## Syncing Test Folders/Modules

All test folders created in synced projects in TestProject will be synced into the corresponding qTest project's Test Design as a module, under a parent module named "TestProject":

![A folder called "Test Folder" is created in TestProject, in a project synced from qTest](<../.gitbook/assets/image (95) (2).png>)

![This "Test Folder" is synced from TestProject and created as a module in Test Design, in the corresponding project.](<../.gitbook/assets/image (117) (1) (1) (1).png>)

The test module data synchronized to qTest will be as follows:&#x20;

* Module Name (from Test Folder Name in TestProject)
* Module Description (from Test Folder Description in TestProject)

{% hint style="info" %}
You can move synced modules in qTest without affecting the results of the synchronization.  If you delete synced modules in qTest, they will likely be repopulated in the next synchronization from TestProject.
{% endhint %}

## Syncing Test Cases

All test cases created in synced projects in TestProject will be synced into the synced qTest modules in Test Design, under a parent module named "TestProject":

!["Test #1" created in TestProject.](<../.gitbook/assets/image (95) (2) (1).png>)

!["Test #1" synced into qTest, in the newly synced "Test Folder" module.](<../.gitbook/assets/image (117) (1) (1).png>)

The test case data synchronized to qTest will be as follows:&#x20;

* Test Name (from Test Name in TestProject)
* Test Description (including URL/app tested, and Test Description in TestProject)
* Test Steps (including navigation, action, parameters, timeout logic, and screenshot logic in TestProject)
* Expected Results (including "Invert Step Result", from TestProject's test step description

With each update to a test case in TestProject, a new test version will be created and approved in qTest.&#x20;

{% hint style="info" %}
Test case data only flows from TestProject to qTest.  Any updates to synchronized test case data in qTest will not be reflected back into TestProject.
{% endhint %}

## Syncing Test Jobs/Cycles

All test jobs created in synced projects in TestProject will become test cycles in Test Execution.  These cycles will have child suites below them which are organized by browser (for web tests) or device (for mobile tests):

![Test Job "Demo Web Tests" created in TestProject.](<../.gitbook/assets/image (169) (2) (1).png>)

![Test Cycle "Demo Web Tests" synced into qTest, with test suites for browsers created as children.](<../.gitbook/assets/image (61).png>)

The test cycle data synchronized to qTest will be as follows:&#x20;

* Test Cycle Name (from Test Job Name in TestProject)
* Test Suite Name (from browsers selected in Test Job in TestProject)

{% hint style="info" %}
Test Cycles can be moved to other Releases/Test Cycles without impacting data synchronization.  Deleting test cycles will likely result in those Test Cycles being regenerated on the following synchronization.
{% endhint %}

{% hint style="info" %}
Any ad-hoc executions in TestProject (i.e. directly from the test case) will be synced into a qTest test cycle named "Jobless Executions."
{% endhint %}

## Syncing Test Suites/Runs

All tests executed in synced projects in TestProject will become test runs in Test Execution (in the corresponding test cycles/test suites.  These runs will have corresponding test logs created within them for each subsequent execution:

!["Test#1" executed in test job "Demo Web Tests" in TestProject.](<../.gitbook/assets/image (169) (2).png>)

!["Test #1" synced into test cycle and suite in qTest, with a test log created for each subsequent run.](<../.gitbook/assets/image (19).png>)

The test run data synchronized to qTest will be as follows:&#x20;

* Test Run Name (from Test Name in TestProject)
* Test Run Description (from Test Description in TestProject), including link to Test Execution Report in TestProject
* Test Step Status (from Test Step Status in TestProject)

{% hint style="info" %}
The first execution of a test in TestProject will create both a test run and a test log in qTest's Test Execution area.  In the subsequent executions, only a test log will be created on the existing test run.
{% endhint %}

## Scheduling Test Executions

Customers using both TestProject and qTest will have a variety of options which they can choose from to execute tests:&#x20;

1. Use TestProject's existing [job scheduling functionality](https://docs.testproject.io/schedule-and-run-tests/create-and-schedule-jobs)
2. Use TestProject's existing [integration to Jenkins](https://docs.testproject.io/testproject-integrations/integration-with-jenkins)
3. Build a custom integration to TestProject using [TestProject's API](https://api.testproject.io/docs/v2/#/Jobs/Jobs\_RunJobAsync), to schedule and execute tests from other CI/CD tools or qTest Launch
