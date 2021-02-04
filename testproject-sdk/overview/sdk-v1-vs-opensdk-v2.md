# SDK \(v1\) vs. OpenSDK \(v2\)

Recently we’ve released a completely new and open-source SDK \(v2\), the OpenSDK. The philosophy behind OpenSDK is to have a single SDK that is as close as possible to the standard Selenium and Appium, allowing users to easily integrate it into existing automation frameworks while utilizing TestProject’s Agent powers for **driver management, single-click configuration,** and **automatic reporting** features.

When working with OpenSDK to develop and execute Web, Android, or iOS tests, all that is required to have a completely managed Selenium/Appium experience is an installation of the [TestProject Agent](https://docs.testproject.io/testproject-agents/what-is-a-testproject-agent), and that’s it!

* Save time & effort by downloading different Selenium drivers or configuring Appium. Everything is handled automatically by the TestProject Agent.
* You can use any unit test framework: Junit, TestNG, Nunit, Mstest, pytest, unittest, etc.
* You can use BDD libraries: SpecFlow, Cucumber, Behave.
* Uploading Tests to the platform is optional, you can execute and debug your tests locally 
* Get automatic reporting, screenshots and tests results in TestProject cloud-based dashboard

**What about the standard SDK \(v1\)?**

SDK v1 allows you to package and upload your test binaries \(C\# DLL/Java JAR files\) to TestProject’s cloud platform as “Coded Tests”. From that moment, TestProject is responsible for distributing and deploying your tests across multiple Agents. Although SDK v1 is based on Selenium and Appium APIs as well, it uses additional layers of interfaces for supporting the automatic distribution. Thus, users who have existing frameworks may require extra effort adjusting it.

**TestProject SDK \(v1\) vs. OpenSDK \(v2\) – Summary**

Below is a short summary of key differences between the two:

| **Feature** | **TestProject SDK v1** | **OpenSDK v2** |
| :--- | :--- | :--- |
| Selenium driver management for all browsers | Supported | Supported |
| Appium driver management for iOS and Android | Supported | Supported |
| Support for iOS on Windows | Supported | Supported |
| Usage within existing automation framework | Requires some Effort | Seamless Support |
| Automatic step execution reporting | Not supported | Supported |
| Local execution with automatic reporting | Only for C\# | Supported |
| C\# Support | Supported | Supported |
| Java Support | Supported | Supported |
| Python Support | Not Supported | Supported |
| Automatic deployment and execution | Supported | Java OpenSDK  |
| WebDriver custom capabilities | Not Supported | Supported |

**Conclusion**

TestProject Addons should be developed with TestProject SDK V1 \(Java\).

**Java** - both SDKs support tests artifacts upload to the platform, this feature \(if required\) can help with test artifacts distribution by the TestProject platform which can simplify the automation CI process.  

**C\#** - Upload to the platform supported only with SDK v1 \(support for OpenSDK will be added soon\)

**Python**  - upload tests to the platform is not supported at the moment. 

