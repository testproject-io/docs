---
description: >-
  Synchronize TestProject test results into qTest for added traceability,
  reporting, and out of the box integration to tools like JIRA.
---

# qTest Integration

## What is qTest?

The **qTest** platform, offered by Tricentis, provides Agile teams with a suite of software testing tools designed to improve speed, efficiency and collaboration throughout the software testing lifecycle.  The platform's flagship product, **qTest Manager** transforms the test case management process, helping enterprise teams get faster and more efficient.  Additionally, **qTest Insights** gives the testing team a self-service business intelligence tool to consolidate, manage and analyze all your test metrics.

## Why do I need qTest Integration?

By integrating **qTest** with TestProject, users will get a number of additional features not included in TestProject, including: 

* Support for manual testing, with a dedicated repository of manual tests and results in **qTest Manager**
* Out of the box integration and traceability to JIRA, Rally, and VersionOne for defects and requirements management
* Fully customizable reports and dashboards for all test results via **qTest Insights**

## Is qTest included with TestProject?

**qTest** and TestProject are separately licensed and deployed products.  **qTest** is a commercial tool which has a separate license and fee from TestProject.  A [free trial ](https://www.tricentis.com/software-testing-tool-trial-demo/qtest-trial/)of **qTest** is available for 14 days via the Tricentis website.

The **qTest** integration is compatible with any **qTest** Cloud Elite or Cloud Trial licenses.  Future plans are being made to make this feature available to **qTest** On-Premise Elite customers.

## How are qTest and TestProject accounts integrated?

**qTest** users that create a TestProject account from the 9-box will be integrating their **qTest** instance \(site\) with a newly created TestProject instance.  From that point forward, all newly created TestProject users from that **qTest** instance will be added to the same TestProject instance.

Once an integration is initiated, the **qTest** artifacts that will be integrated with TestProject include:

* **Projects:** new projects will be created in TestProject every time to align with the existing **qTest** project hierarchy.  Users can also create projects directly in TestProject, which will not be integrated back to **qTest**
* **Test Suites** \(**coming soon\):** any new jobs created in TestProject will be synchronized and created as Test Suites in their corresponding projects in **qTest**
* **Test Runs/Logs \(coming soon\):** any new test runs \(within a job\) created in TestProject will be synchronized to **qTest** as Test Runs/Logs and organized in the proper suites \(which relate to TestProject jobs\)
* **Test Cases \(coming soon\):** for any executed jobs in TestProject, the corresponding test cases will be created in qTest and organized in a separate module named "TestProject".

## Setting up qTest Integration

Users of **qTest** \(Cloud Elite or Cloud Trial\) should now see the TestProject icon within their 9-box:

![TestProject logo within the qTest 9-box.](../.gitbook/assets/image%20%28170%29.png)

Clicking on the TestProject logo within the **qTest** 9-box will trigger the account creation process in TestProject for that **qTest** user**.**  First, TestProject will check to see if there is an existing TestProject account for that **qTest** user's email address.

If the **qTest** user's email is already established as a user in TestProject, TestProject will skip forward to integrating that TestProject account to the **qTest** account.

If the **qTest** user's email is not yet established as a user in TestProject, TestProject will automatically initiate the process of creating an integrated TestProject account with that user's email address.  First, the user must validate their email address:

![Notification of email validation send to the newly created TestProject user. ](../.gitbook/assets/image%20%28121%29.png)

Then, the user must click the link in the email from TestProject to validate their email address:

![Email validation sent to the user.](../.gitbook/assets/image%20%28189%29.png)

{% hint style="info" %}
If you do not receive the validation email, please contact us at support@testproject.io to manually validate your email.
{% endhint %}

Finally, the user must accept TestProject's separate Terms of Service related to the separate TestProject free license before their account is fully activated and ready to be used:

![TestProject Terms of Service, which must be agreed to for account activation.](../.gitbook/assets/image%20%2810%29.png)

From this point, the integration is automatically set, according to default settings.  You should see the TestProject projects list populated with projects from qTest.  

In the coming week, you will be able to make further configuration and also should start seeing other artifacts \(jobs, test cases, and test results\) populating in **qTest.**  Upon release of this feature, TestProject will be able to synchronize the historical results into **qTest**, so there is no need to worry about losing the results of any tests you create now.



