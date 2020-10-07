# SDK \(v1\) vs. OpenSDK \(v2\)

Recently we’ve released a completely new and open source SDK \(v2\), the OpenSDK. The philosophy behind OpenSDK is to have a single SDK that is as close as possible to the standard Selenium and Appium, allowing users to easily integrate it into existing automation frameworks, while utilizing TestProject’s Agent powers for: **driver management, single click configuration** and **automatic reporting** features.

When working with OpenSDK to develop and execute Web, Android or iOS tests, all that is required to have a completely managed Selenium/Appium experience is an installation of the [TestProject Agent](https://docs.testproject.io/testproject-agents/what-is-a-testproject-agent), and that’s it!

* Save time & effort of downloading different Selenium drivers or configuring Appium. Everything is handled automatically by the TestProject Agent.
* You can use any framework or 3rd party tools: Unit testing frameworks, Cucumber, SpecFlow, Junit, TestNG, etc.
* No need to upload anything to the TestProject Cloud or integrating reporters of any kind.
* You will benefit from beautiful test reports that are automatically created for you on TestProject’s reporting dashboard, where you will be able to also download them in PDF format.

**What about the standard SDK \(v1\)?**

SDK v1 allows you to package and upload your binaries \(C\# DLL/Java JAR files\) to TestProject’s cloud platform as “Coded Tests”. From that moment, TestProject is responsible for distributing and deploying your tests across multiple Agents. Although SDK v1 is based on Selenium and Appium APIs as well, it uses additional layers of interfaces for supporting the automatic distribution. Thus, users who have existing frameworks may require extra effort adjusting it.

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
| Automatic deployment and execution | Supported | Not yet Supported _**\[1\]**_ |
| WebDriver custom capabilities | Not Supported | Supported |

**Conclusion**

If you are utilizing the upload code feature and coded tests deployment by TestProject platform – then SDK v1 is for you. However, if you are looking to enrich your existing platform with the power of automatic reporting and driver management, while having a flexibility framework with your own build and deployment pipelines \(while storing the artifacts locally\) – you should probably try the OpenSDK \(v2\).  


_**\[1\]**_  Automatic deployment and execution will be implemented for the OpenSDK in the future.  
Automatic deployment and execution \(currently only supported with SDK v1\) refers to uploading the code to the TestProject cloud platform to be able to schedule the execution of the code. For example, when you add a test in a Job, you enable TestProject to manage the deployment of the test. When you upload the code, you simply press a button and the code executes from the platform on your machine, meaning that TestProject handles the pipeline from the moment when you start the test until the test executes.

Using the OpenSDK \(v2\), executions are local so the flow of the test execution is on the side of the developer, as well as the deployment. Some can find if better since they have existing pipelines for deployment and they don't require TestProject for handling that.

