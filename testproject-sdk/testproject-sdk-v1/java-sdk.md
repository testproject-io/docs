---
description: Java SDK (v1)
---

# Java

This repository contains code examples based on TestProject Java SDK.

## Briefing

This document describes the bare minimum steps to start developing tests using the Java SDK.\
&#x20;TestProject provides a unified test automation SDK with support for Android, iOS and Web applications by utilizing the open-source Selenium and Appium frameworks. TestProject is OS agnostic and can run on Windows, Linux or Mac. It is a full stack automation framework with capabilities that allow automation test management, remote and local test execution, job scheduling, reporting dashboards, collaboration and more.

## Preparations

To kick-off automation development with TestProject, it is necessary to have an active TestProject account and the TestProject Agent installed.\
&#x20;TestProject's Agent is a cross-platform desktop application, allowing you to create, debug and execute your test automation locally. TestProject Agent can be downloaded from [Agents](https://app.testproject.io/#/agents) page.

### Getting Java SDK

You can download TestProject SDK for Java from the [Developers](https://app.testproject.io/#/integrations/develop-addon) page and reference it in your project.

#### Installing SDK

To use TestProject SDK you have to add it as a reference to your project.\
&#x20;Here are some examples for how it should be done using Maven or Gradle.

Maven:

```
<dependency>
    <groupId>io.testproject</groupId>
    <artifactId>java-sdk</artifactId>
    <version>1.0</version>
    <systemPath>/path/to/sdk/io.testproject.sdk.java.jar</systemPath>
    <scope>system</scope>
</dependency>
```

Gradle:

```
 compile files("/path/to/sdk/io.testproject.sdk.java.jar")
```

Refer to _pom.xml_ and _build.gradle_ files in the provided examples for more details.

## Test Development

The best way to start developing automated tests with TestProject is by reviewing the source code of a basic test that performs a login and updates a profile form, expecting the save to succeed.

* [Web](https://github.com/testproject-io/java-sdk-examples/blob/master/Web/Test/src/main/java/io/testproject/examples/sdk/tests/BasicTest.java) test executed on [TestProject Demo](https://example.testproject.io/web/index.html) website.
* [Android](https://github.com/testproject-io/java-sdk-examples/blob/master/Android/Test/src/main/java/io/testproject/examples/sdk/tests/BasicTest.java) test executed on [TestProject Demo](https://github.com/testproject-io/android-demo-app) App for Android.
* [iOS](https://github.com/testproject-io/java-sdk-examples/blob/master/iOS/Test/src/main/java/io/testproject/examples/sdk/tests/BasicTest.java) test executed on [TestProject Demo](https://github.com/testproject-io/ios-demo-app) App for iOS.

There is also a [Generic](https://github.com/testproject-io/java-sdk-examples/blob/master/Generic/Test/src/main/java/io/testproject/examples/sdk/tests/BasicTest.java) test, representing a dummy scenario that can be automated.\
&#x20;It can be used as a reference for real scenarios that automate a non-UI sequences (those that do not require a Selenium or Appium driver).

### Test Class

In order to build a Test that can be executed by TestProject, the class has to implement on of the interfaces that the SDK provides.\
&#x20;Interface implementation requires an implementation of the _execute()_ method, that will be be invoked by the platform to run the Test.\
&#x20;The _execute()_ method returns _ExecutionResult_ enum which can be **PASSED** or **FAILED**.

Below are some examples for Test implementation on different platforms:

**Web Test**

BasicTest class implements the _WebTest_ interface:

```
public class BasicTest implements WebTest
```

Test entry point is the _execute_ method:

```
public ExecutionResult execute(WebTestHelper helper) throws FailureException
```

The following line of code retrieves a driver to automate the browser.

```
// Get driver initialized by TestProject Agent
// No need to specify browser type, it can be done later via UI
WebDriver driver = helper.getDriver();
```

Following code is used to navigate the browser to the relevant URL. After it is executed, TestProject Demo page is loaded.

```
// Navigate to TestProject Demo website
driver.navigate().to("https://example.testproject.io/web/");
```

The following code uses the Page Object Model pattern to login in and complete a profile form, saving it:

```
// Login using provided credentials
LoginPage loginPage = PageFactory.initElements(driver, LoginPage.class);
loginPage.login(name, password);

// Complete profile forms and save it
ProfilePage profilePage = PageFactory.initElements(driver, ProfilePage.class);
profilePage.updateProfile(country, address, email, phone);
```

The following return statement will assert test result:

```
return profilePage.isSaved() ? ExecutionResult.PASSED : ExecutionResult.FAILED;
```

**Android Test**

BasicTest class implements the _AndroidTest_ interface:

```
public class BasicTest implements AndroidTest
```

Test entry point is the _execute_ method:

```
public ExecutionResult execute(AndroidTestHelper helper) throws FailureException
```

The following line of code retrieves a driver to automate the App.

```
// Get driver initialized by TestProject Agent
AndroidDriver driver = helper.getDriver();
```

The following code resets the App and uses the Page Object Model pattern to login in and complete a profile form, saving it:

```
 driver.resetApp();

LoginPage loginPage = new LoginPage(driver);
loginPage.login(name, password);

ProfilePage profilePage = new ProfilePage(driver);
profilePage.updateProfile(country, address, email, phone);
```

The following return statement will assert test result:

```
return profilePage.isSaved() ? ExecutionResult.PASSED : ExecutionResult.FAILED;
```

**iOS Test**

BasicTest class implements the _IOSTest_ interface:

```
public class BasicTest implements IOSTest
```

Test entry point is the _execute_ method:

```
public ExecutionResult execute(IOSTestHelper helper) throws FailureException
```

The following line of code retrieves a driver to automate the App.

```
// Get driver initialized by TestProject Agent
IOSDriver driver = helper.getDriver();
```

The following code resets the App and uses the Page Object Model pattern to login in and complete a profile form, saving it:

```
 driver.resetApp();

LoginPage loginPage = new LoginPage(driver);
loginPage.login(name, password);

ProfilePage profilePage = new ProfilePage(driver);
profilePage.updateProfile(country, address, email, phone);
```

The following return statement will assert test result:

```
return profilePage.isSaved() ? ExecutionResult.PASSED : ExecutionResult.FAILED;
```

**Generic Test**

BasicTest class implements the _GenericTest_ interface:

```
public class BasicTest implements GenericTest
```

Test entry point is the _execute_ method:

```
public ExecutionResult execute(TestHelper helper) throws FailureException
```

The following code adds the value stored in 'a' variable to the value in 'b' and if equals 2, asserts success:

```
int a = 1, b = 1;

if (a + b == 2) {
    return ExecutionResult.PASSED;
} else {
    return ExecutionResult.FAILED;
}
```

### Debugging / Running Test

To debug or run the test locally, you will have to use the _Runner_ class from TestProject SDK. All code examples, have JUnit tests that use _Runner_ to debug the automation locally. Debugging or running a test locally with the _Runner_ class, requires authentication before communication with the TestProject Agent (since it is the execution engine). Development token for authentication can be easily obtained from the [Developers](https://app.testproject.io/#/developers) page. It should be used as a parameter in one of the _Runner_ factory methods:

**Web**

```
Runner runner = Runner.createWeb("YOUR_DEV_TOKEN", ...
```

**Android**

```
Runner runner = Runner.createAndroid("YOUR_DEV_TOKEN", ...
```

**Chrome on Android**

```
Runner runner = Runner.createAndroidWeb("YOUR_DEV_TOKEN", ...
```

**iOS**

```
Runner runner = Runner.createIOS("YOUR_DEV_TOKEN", ...
```

**Safari on iOS**

```
Runner runner = Runner.createIOSWeb("YOUR_DEV_TOKEN", ...
```

**Generic**

```
Runner runner = Runner.create("YOUR_DEV_TOKEN"...
```

### Using parameters and step reports in your tests

Let's make our example more advanced by adding parameters. To add parameters to your test, you simply need to add fields with relevant annotations.\
&#x20;In addition, we will create step reports to separate the different stages of the test (each report will appear as a separate step in the future execution reports).

See the relevant platform link for full source code:

* [Web - Extended Test](https://github.com/testproject-io/java-sdk-examples/blob/master/Web/Test/src/main/java/io/testproject/examples/sdk/tests/ExtendedTest.java)
* [Android - Extended Test](https://github.com/testproject-io/java-sdk-examples/blob/master/Android/Test/src/main/java/io/testproject/examples/sdk/tests/ExtendedTest.java)
* [iOS - Extended Test](https://github.com/testproject-io/java-sdk-examples/blob/master/iOS/Test/src/main/java/io/testproject/examples/sdk/tests/ExtendedTest.java)
* [Generic - Extended Test](https://github.com/testproject-io/java-sdk-examples/blob/master/Generic/Test/src/main/java/io/testproject/examples/sdk/tests/ExtendedTest.java)

#### Test Annotations

TestProject SDK provides annotations to describe the test and its parameters:

1. The _**Test**_ annotation is used to better describe the Test and define how it will appear later in TestProject UI:
   * **name** - The name of the test (if omitted, the name of the class will be used).
   * **description** - A description of the test which is shown in various places in TestProject platform (e.g. reporting dashboard). The description may contain placeholders {{propertyName}} that will be changed dynamically according to test parameters.
   * **version** - A version string which is used for future reference.
2. The _**Parameter**_ annotation is used to better describe your Test inputs and outputs, in the example above there are two inputs - _url_ and _expectedTitle_.
   * **description** - The description of the parameter
   * **direction** - Defines the parameter as an _input_ (default if omitted) or an _output_ parameter. An _input_ parameter will receive values when the test is executed while the _output_ parameter value will be retrieved at the end of test execution (and can be used in following steps later on in the automation scenario).
   * **defaultValue** - Defines a default value that will be used for the parameter.

#### Reports

Implemented _execute()_ method receives a _Helper_ instance as a parameter.\
&#x20;Via this helper, you can obtain an instance of _TestReporter_ class.

```
TestReporter report = helper.getReporter();
```

Notice the following line in the Extended Test example.\
&#x20;This line reports a step based on provided condition and takes a screenshot:

```
report.step("Profile information saved", profilePage.isSaved(), TakeScreenshotConditionType.Always);
```

Using the following code one can set test result message:

```
report.result("Test completed successfully");
```

## Addon development

Much like tests, you can develop custom Addons to extend TestProject and shape your automated testing solution for your needs. An Addon is a set of Actions (one or more) where each Action does a specific task. A common Addon scenario will be to extend basic set of Actions on complicated UI elements or make wrappers for user defined API. Once created, Actions can be used to design steps of automated tests.

You can learn more about how to create your own addons, [here ](../../testproject-addons/develop-an-addon/)in the documentation.

## Crowd Code / Addon Proxy

One of the greatest features of the TestProject environment is the ability to execute a code written by someone else.\
&#x20;It can be your account colleagues writing actions that you can reuse, or TestProject community users.\
&#x20;Developer must download a binary file with the proxy class for the Action he wants to execute.

Assuming your account member uploaded the example Addon, named it _**Example**_ and you want to reuse it's code your Test.\
&#x20;To do so, you can download it's proxy JAR and use it like this:

```
ClearFields clearFieldsAction = ExampleAddon.clearFields();
```

Implemented _execute()_ method receives a _Helper_ instance as a parameter.\
&#x20;Via this helper, you can execute the proxy by invoking the _**executeProxy**_ method:

```
StepExecutionResult result = helper.executeProxy(clearFieldsAction);
```

See examples:

* [Web - Proxy Test](https://github.com/testproject-io/java-sdk-examples/blob/master/Web/Test/src/main/java/io/testproject/examples/sdk/tests/ProxyTest.java)
* [Android - Proxy Test](https://github.com/testproject-io/java-sdk-examples/blob/master/Android/Test/src/main/java/io/testproject/examples/sdk/tests/ProxyTest.java)
* [iOS - Proxy Test](https://github.com/testproject-io/java-sdk-examples/blob/master/iOS/Test/src/main/java/io/testproject/examples/sdk/tests/ProxyTest.java)
* [Generic - Proxy Test](https://github.com/testproject-io/java-sdk-examples/blob/master/Generic/Test/src/main/java/io/testproject/examples/sdk/tests/ProxyTest.java)

## Packaging

To package and upload coded tests written using the **TestProject V1 SDK** in **Java**, you will need to package it as a **.jar** file.&#x20;

Export your code as an uber .jar file with dependencies, excluding the TestProject SDK.

Once the jar is compiled and uploaded, TestProject will display your project as a package with **all** the tests inside of it.

Please note that once uploaded, the tests **cannot be edited unless reuploaded** after performing the changes in your local development environment.

The following examples have been created using **IntelliJ**.

_**Gradle**_

Open the Gradle tab in your IDE, you will need to compile a jar using **Tasks/build/jar**.

![](<../../.gitbook/assets/1 (4).png>)

After running the task, the jar will be created in the **build/libs** directory.

![](<../../.gitbook/assets/2 (4).png>)

_**Maven**_

Open the Maven tab, select **Lifecycle**, and execute the following in order:

* clean
* compile
* package

![](<../../.gitbook/assets/3 (5) (1) (1).png>)

Once the package command ends; the jar will be created in the **target** directory.

![](<../../.gitbook/assets/4 (5).png>)

To upload the package, head to your project on the TestProject platform, and create a **new test**.

![](<../../.gitbook/assets/5 (5).png>)

Select the **code** option.

![](<../../.gitbook/assets/6 (4).png>)

**Upload** your jar.

![](<../../.gitbook/assets/7 (4).png>)

Press **next**.

![](<../../.gitbook/assets/8 (3).png>)

Give your package a **name**, **description** and choose an **application** and press next to complete the process.

![](<../../.gitbook/assets/9 (3).png>)

See build.gradle or pom.xml files in code examples for details on how to include the TestProject V1 SDK dependency in your project.

## Support

For any further inquiries, please use TestProject support channels:

* [Forum](https://forum.testproject.io)
* In-app Chat
* Email at support@testproject.io
