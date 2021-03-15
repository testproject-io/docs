# Legacy SDK vs. OpenSDK

Recently we’ve released a completely new and open-source SDK \(v2\), the OpenSDK. The philosophy behind OpenSDK is to have a single SDK that is as close as possible to the standard Selenium and Appium, allowing users to easily integrate it into existing automation frameworks while utilizing TestProject’s Agent powers for **driver management, single-click configuration,** and **automatic reporting** features.

When working with OpenSDK to develop and execute Web, Android, or iOS tests, all that is required to have a completely managed Selenium/Appium experience is an installation of the [TestProject Agent](https://docs.testproject.io/testproject-agents/what-is-a-testproject-agent), and that’s it!

* Save time & effort by downloading different Selenium drivers or configuring Appium. Everything is handled automatically by the TestProject Agent.
* You can use any unit test framework: Junit, TestNG, Nunit, Mstest, pytest, unittest, etc.
* You can use BDD libraries: SpecFlow, Cucumber, Behave.
* Uploading Tests to the platform is optional, you can execute and debug your tests locally 
* Get automatic reporting, screenshots and tests results in TestProject cloud-based dashboard

**What about the TestProject Legacy SDK?**

The Legacy SDKs and the OpenSDKs allow you to package and upload your test binaries \(C\# DLL/Java JAR files\) to TestProject’s cloud platform as “Coded Tests”. From that moment, TestProject is responsible for distributing and deploying your tests across multiple Agents. Although the Legacy SDK is based on Selenium and Appium APIs as well, it uses additional layers of interfaces for supporting the automatic distribution. Thus, users who have existing frameworks may require extra effort to adjust them.

{% hint style="info" %}
The Legacy SDKs are used exclusively for creating Addons.
{% endhint %}

\*\*\*\*

**TestProject Legacy SDK vs. OpenSDK  – Summary**

Below is a short summary of key differences between the two:

| **Feature** |  **Legacy SDK** | **OpenSDK** |
| :--- | :--- | :--- |
| Selenium driver management for all browsers | Supported | Supported |
| Appium driver management for iOS and Android | Supported | Supported |
| Support for iOS on Windows | Supported | Supported |
| Usage within an existing automation framework | Requires some Effort | Seamless Support |
| Automatic step execution reporting | Not supported | Supported |
| Local execution with automatic reporting | Only for C\# | Supported |
| C\# Support | Supported | Supported |
| Java Support | Supported | Supported |
| Python Support | Not Supported | Supported |
| Automatic deployment and execution | Supported | Java OpenSDK, C\# OpenSDK  |
| WebDriver custom capabilities | Not Supported | Supported |

**Conclusion**

TestProject Addons should be developed with TestProject Legacy SDK \(Java, C\#\).

**Java, C\#** - both SDKs support test artifacts upload to the platform, this feature \(if required\) can help with test artifacts distribution by the TestProject platform which can simplify the automation CI process.  

**Python**  - upload tests to the platform is not supported at the moment. 

