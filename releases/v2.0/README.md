---
description: Version 2.0 - Release Notes
---

# v2.0

This major new **TestProject 2.0** **version** is packed with a bunch of awesome new features and improvements _\*\*_we know you've all been waiting for! From now on, you can enjoy the best of both worlds with TestProject! Whether you need the simplicity of a cloud solution or the control of hosting tests locally – we’ve got you covered. You can read more in the release notes below or on our [announcement blog](https://blog.testproject.io/2021/03/16/announcing-testproject-next-gen-release-hybrid-cloud-and-offline-mode/).

## New Features and Improvements

**Save Tests Locally** - We are always there for our community and we want everyone to find TestProject useful and to be able to utilize all the great features the platform provides. For this reason, we've added an easy way to save your tests locally on your drive. After you record a test, you can choose the "Save to File" option from the test context menu. This will result in a YAML file that can be easily stored locally or in your GIT repository to allow you to version control your tests. The local tests can be executed using the brand new TestProject [Agent CLI](https://docs.testproject.io/testproject-agents/testproject-agent-cli) capabilities. This combination allows you for example to attach your tests to your code repository and run them locally as a part of the CI process for a specific version of your application as you do with unit tests. By the way, test import is coming soon!

**Offline Recording** - In addition to the above, you can utilize the in-browser recorder to create powerful on-premise tests extended by the largest library of automation [addons](https://addons.testproject.io). Save tests locally on your machine for backup, version management, and complete offline execution. This means that you can use our advanced recorder to create local tests without saving them to the cloud as well. To create such tests just use the normal "New Test" flow and choose "File" on the final step. You can later edit your local tests as well by clicking the "Open Test" button on the top of the screen.

![](https://storage-static.testproject.io/release-notes/2.0/local-test.png)

**Your Wish Is My Command!** - Our agent just got greater! We are very excited to tell you that the TestProject agent now has a CLI. It is a cross-operating system command-line interface utility and it's made for the execution of test packages generated using the TestProject platform. As mentioned above, tests that are saved to a file or created using offline recording can be easily executed by agent commands in addition to some other cool commands that can help you rapidly move forward with automating your tests. The complete documentation can be found [here](https://docs.testproject.io/testproject-agents/testproject-agent-cli)

**Offline Agent** - You asked for it, and we listened! One of our most requested features was to enable TestProject to operate completely offline while still benefiting from all its powerful capabilities. We are glad to announce that TestProject 2.0 Agent does exactly that meaning that you can run your local tests without connecting our agent to the cloud. You can read more about it on our [blog](https://blog.testproject.io/2021/03/16/announcing-testproject-next-gen-release-hybrid-cloud-and-offline-mode/).

**Tags Are The Best!** - Going forward with automation projects it can get difficult to manage your automation components. We understand that and are constantly working towards improving usability to allow our users to focus on building great automated tests and not worry about anything else. In this version we've introduces Tags that we think will make lives easier. You can now define tags on tests, jobs, agents, and executions. When creating/editing tests and jobs, just define up to 10 short tags (20 chars max). Once it is there, you will be able to search for them to quickly find what you are looking for. Soon, we will also add advanced filtering options to take it even further. In addition to that, when executing your jobs or tests using our [REST API](https://api.testproject.io/docs/v2/#/), you can send a list of tags to be included in the execution. After your automation finished running, all the tags will be visible in the report and you can easily filter your executions by these tags.

![](https://storage-static.testproject.io/release-notes/2.0/job-tags.png)

![](https://storage-static.testproject.io/release-notes/2.0/test-tags.png)

![](https://storage-static.testproject.io/release-notes/2.0/agent-tags.png)

![](https://storage-static.testproject.io/release-notes/2.0/report-tags.png)

**Keep it stable** - In addition to all the great stuff mentioned above, we've made some major enhancements to make our agent even more stable and seamless than it already is! In addition to this, we've completely switched to W3C to be compliant with the latest and greatest technology.

## Fixes

### Agent

* Docker agent was getting stuck after few days of inactivity
* Registration got stuck for a long time on some Mac machines
* Environment RAM on the Agent tab was incorrect

### Execution

* Coded tests were not executing on some Cloud targets

### Recorder

* Failed steps were shown as recovered

### SDK & Code

* Python code generation resulted in an error for some tests

## Supported Browsers

### Installed Browsers

* Chrome **77+**
* FireFox **60+**
* Safari **12+**
* Edge **44+**
* Internet Explorer **11**

### Sauce Labs Browsers

* Chrome **75+**
* FireFox **60+**
* Safari **12+**
* Edge **44+**
* Internet Explorer **11**

## Supported Devices

* Android: **5.0** _(Lollipop)_ - **11.0**
* iOS: **10** - **14.4**

## Supported Agent Operating Systems (x64 only)

* Windows 7, 8, 8.1, 10
* macOS 10.14+
* Ubuntu 16.04, 18.04, 20.04

## Supported Emulators Frameworks

* Android Studio Latest
* Genymotion Latest
* XCode **10-12.4**
