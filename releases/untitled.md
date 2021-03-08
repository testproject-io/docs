---
description: Version 0.66 - Release Notes
---

# v0.66

### New Features and Improvements

**Automation Assistant** - In the last few versions we've introduced various [AI capabilities](https://testproject.io/ai-tools/) like self-healing elements and an advance adaptive wait mechanism, and we are not stopping there. In this version, we've added the automation assistant. The automation assistant was created to reduce test flakiness \(for example, actions that are reported as passed but didn’t actually do what they were supposed to\). The assistant achieves this by analyzing each step and detecting cases where an action didn’t reach its target goal, then attempts to fix it automatically. This feature is automatically enabled for all new tests, so you don't have to do anything special. If you wish to disable it, just go to test settings and turn it off. Read more in [this detailed blog post](https://blog.testproject.io/2021/01/20/free-appium-ai-tools-for-mobile-testing-finally-here/).

**Bring it on!** - Following the release of our [OpenSDK](https://docs.testproject.io/testproject-sdk/opensdk-v2), we are happy to say that you can now upload Java and C\# tests that were written using one of them to TestProject platform. No matter which test framework you use, all the tests will be reflected in the cloud and you and your teammates will be able to easily run them from anywhere.

**BDD Style** - Our OpenSDK now supports various [BDD](https://docs.testproject.io/testproject-sdk/behavior-driven-development) frameworks to allow you to do what you know and love while utilizing all the benefits for TestProject. Check out the documentation for [C\# SpecFlow](https://docs.testproject.io/testproject-sdk/behavior-driven-development/c-and-specflow-bdd), [Java Cucumber](https://docs.testproject.io/testproject-sdk/behavior-driven-development/cucumber-java), and [Python Behave](https://docs.testproject.io/testproject-sdk/behavior-driven-development/behave-python) for more info and examples.

**Show me the Code** - Python is often being used by automation developers which are an important part of our growing community, so it was a logical choice to add the Python code generation in addition to the existing Java and C\# options.

**Reporting & Dashboards Facelift** - Reporting plays a huge role in our day-to-day testing and debugging efforts. We know just how crucial it is to have detailed test reports that you can trust, so we've made it a high priority to provide just that. We gave our existing reports a whole new look & feel and fixed some UX issues to provide you with the best reporting experience possible.

### Fixes

#### Agent

* _"Failed to create driver session"_ when running second time on different iOS simulators
* Agent takes a long time to start sometimes
* Application URL Parameter is ignored on docker agents
* Could not infer Safari browser version
* Docker Agent crash on ubuntu due to _"java.nio.file.NoSuchFileException: /home/agent/.testproject/agent/runtime.json"_ error
* Simulators not detected sometimes
* When mirroring second time on a different simulator, mirroring failed on iOS simulators

#### Execution

* Chrome was not being opened in headless mode when executing Job with Desired Capabilities.
* Edge fails to start on MacOS
* Element locator was not updated after self-healing
* Failed to clear element text
* Failed to use data source with a null error
* Job failed to execute with _moz:firefoxOptions_ capabilities
* Mobile _tap_ fails to find the element while _clicking_ works
* Slow mobile web test execution on iOS devices
* Tap at accessibility ID locator not working, but double-tap at the same accessibility ID does work
* Virtual Agents shows no progress in the monitor

#### Recorder

* Can't capture elements inside a ViewGroup element \(ReactNative app\)
* Chrome recording session is loading forever
* Continue Test does not execute the next steps
* iOS Mirroring Orientation does not change to landscape orientation
* Provisioned iOS device was unable to mirror
* Sometimes, steps were created as self-healed on iOS tests
* Type text \(if visible\) was sometimes failing when running from the recorder

#### SDK & Code

* Python code generation was failing sometimes
* Can't execute iOS tests locally with Java OpenSDK
* Failed to communicate with the Agent
* IE Options were ignored in OpenSDK
* If OpenSDK fails to open a DEV session for any reason, the test isn't reported as failed
* Java OpenSDK uploaded code fails to run
* Java SDK fails to report correct test names
* Uploaded Java OpenSDK code - Job report is wrong
* Uploaded Java OpenSDK for Android tests in Android job is failing with a null error
* Web development sessions do not open with the excuse that the current session is not the same as the requested session

#### Reports

* In some situations, large reports were not uploaded to the platform
* OpenSDK Coded tests and steps have no duration in reports
* Report Icon is missing after refreshing
* Reports appear with future dates in some rare cases
* Reports were generated and uploaded to the platform
* Steps marked as _"always pass"_ were marked as _"failed"_ in the report

#### Integrations

* Sauce Labs integration was failing for specific regions

#### Share Center

* Tests shared with addons that are not installed failed to start with a vague message

### Supported Browsers

#### Installed Browsers

* Chrome **77+**
* FireFox **60+**
* Safari **12+**
* Edge **44+**
* Internet Explorer **11**

#### Sauce Labs Browsers

* Chrome **75+**
* FireFox **60+**
* Safari **12+**
* Edge **44+**
* Internet Explorer **11**

### Supported Devices

* Android: **5.0** _\(Lollipop\)_ - **11.0**
* iOS: **10** - **14**

### Supported Agent Operating Systems \(x64 only\)

* Windows 7, 8, 8.1, 10
* macOS 10.14, 10.15
* Ubuntu 16.04, 18.04 

> This document and all previous release notes are also available at the [TestProject documentation portal](https://docs.testproject.io/releases).

