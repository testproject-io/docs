---
description: Java SDK (v1)
---

# Java

This repository contains code examples based on TestProject Java SDK.

## Briefing

This document describes the bare minimum steps to start developing tests using the Java SDK.  
 TestProject provides a unified test automation SDK with support for Android, iOS and Web applications by utilizing the open-source Selenium and Appium frameworks. TestProject is OS agnostic and can run on Windows, Linux or Mac. It is a full stack automation framework with capabilities that allow automation test management, remote and local test execution, job scheduling, reporting dashboards, collaboration and more.

## Preparations

To kick-off automation development with TestProject, it is necessary to have an active TestProject account and the TestProject Agent installed.  
 TestProject's Agent is a cross-platform desktop application, allowing you to create, debug and execute your test automation locally. TestProject Agent can be downloaded from [Agents](https://app.testproject.io/#/agents) page.

### Getting Java SDK

You can download TestProject SDK for Java from the [Developers](https://app.testproject.io/#/developers) page and reference it in your project.

#### Installing SDK

To use TestProject SDK you have to add it as a reference to your project.  
 Here are some examples for how it should be done using Maven or Gradle.

Maven:

```text
<dependency>
    <groupId>io.testprojectgroupId>
    <artifactId>java-sdkartifactId>
    <version>1.0version>
    <systemPath>/path/to/sdk/io.testproject.sdk.java.jarsystemPath>
    <scope>systemscope>
dependency>
```

Gradle:

```text
 compile files("/path/to/sdk/io.testproject.sdk.java.jar")
```

Refer to _pom.xml_ and _build.gradle_ files in the provided examples for more details.

## Test Development

The best way to start developing automated tests with TestProject is by reviewing the source code of a basic test that performs a login and updates a profile form, expecting the save to succeed.

* [Web](https://github.com/testproject-io/java-sdk-examples/blob/master/Web/Test/src/main/java/io/testproject/examples/sdk/tests/BasicTest.java) test executed on [TestProject Demo](https://example.testproject.io/web/index.html) website.
* [Android](https://github.com/testproject-io/java-sdk-examples/blob/master/Android/Test/src/main/java/io/testproject/examples/sdk/tests/BasicTest.java) test executed on [TestProject Demo](https://github.com/testproject-io/android-demo-app) App for Android.
* [iOS](https://github.com/testproject-io/java-sdk-examples/blob/master/iOS/Test/src/main/java/io/testproject/examples/sdk/tests/BasicTest.java) test executed on [TestProject Demo](https://github.com/testproject-io/ios-demo-app) App for iOS.

There is also a [Generic](https://github.com/testproject-io/java-sdk-examples/blob/master/Generic/Test/src/main/java/io/testproject/examples/sdk/tests/BasicTest.java) test, representing a dummy scenario that can be automated.  
 It can be used as a reference for real scenarios that automate a non-UI sequences \(those that do not require a Selenium or Appium driver\).

### Test Class

In order to build a Test that can be executed by TestProject, the class has to implement on of the interfaces that the SDK provides.  
 Interface implementation requires an implementation of the _execute\(\)_ method, that will be be invoked by the platform to run the Test.  
 The _execute\(\)_ method returns _ExecutionResult_ enum which can be **PASSED** or **FAILED**.

Below are some examples for Test implementation on different platforms:

**Web Test**

BasicTest class implements the _WebTest_ interface:

```text
public class BasicTest implements WebTest
```

Test entry point is the _execute_ method:

```text
public ExecutionResult execute(WebTestHelper helper) throws FailureException
```

The following line of code retrieves a driver to automate the browser.

```text
// Get driver initialized by TestProject Agent
// No need to specify browser type, it can be done later via UI
WebDriver driver = helper.getDriver();
```

Following code is used to navigate the browser to the relevant URL. After it is executed, TestProject Demo page is loaded.

```text
// Navigate to TestProject Demo website
driver.navigate().to("https://example.testproject.io/web/");
```

The following code uses the Page Object Model pattern to login in and complete a profile form, saving it:

```text
// Login using provided credentials
LoginPage loginPage = PageFactory.initElements(driver, LoginPage.class);
loginPage.login(name, password);

// Complete profile forms and save it
ProfilePage profilePage = PageFactory.initElements(driver, ProfilePage.class);
profilePage.updateProfile(country, address, email, phone);
```

The following return statement will assert test result:

```text
return profilePage.isSaved() ? ExecutionResult.PASSED : ExecutionResult.FAILED;
```

**Android Test**

BasicTest class implements the _AndroidTest_ interface:

```text
public class BasicTest implements AndroidTest
```

Test entry point is the _execute_ method:

```text
public ExecutionResult execute(AndroidTestHelper helper) throws FailureException
```

The following line of code retrieves a driver to automate the App.

```text
// Get driver initialized by TestProject Agent
AndroidDriver driver = helper.getDriver();
```

The following code resets the App and uses the Page Object Model pattern to login in and complete a profile form, saving it:

```text
 driver.resetApp();

LoginPage loginPage = new LoginPage(driver);
loginPage.login(name, password);

ProfilePage profilePage = new ProfilePage(driver);
profilePage.updateProfile(country, address, email, phone);
```

The following return statement will assert test result:

```text
return profilePage.isSaved() ? ExecutionResult.PASSED : ExecutionResult.FAILED;
```

**iOS Test**

BasicTest class implements the _IOSTest_ interface:

```text
public class BasicTest implements IOSTest
```

Test entry point is the _execute_ method:

```text
public ExecutionResult execute(IOSTestHelper helper) throws FailureException
```

The following line of code retrieves a driver to automate the App.

```text
// Get driver initialized by TestProject Agent
IOSDriver driver = helper.getDriver();
```

The following code resets the App and uses the Page Object Model pattern to login in and complete a profile form, saving it:

```text
 driver.resetApp();

LoginPage loginPage = new LoginPage(driver);
loginPage.login(name, password);

ProfilePage profilePage = new ProfilePage(driver);
profilePage.updateProfile(country, address, email, phone);
```

The following return statement will assert test result:

```text
return profilePage.isSaved() ? ExecutionResult.PASSED : ExecutionResult.FAILED;
```

**Generic Test**

BasicTest class implements the _GenericTest_ interface:

```text
public class BasicTest implements GenericTest
```

Test entry point is the _execute_ method:

```text
public ExecutionResult execute(TestHelper helper) throws FailureException
```

The following code adds the value stored in 'a' variable to the value in 'b' and if equals 2, asserts success:

```text
int a = 1, b = 1;

if (a + b == 2) {
    return ExecutionResult.PASSED;
} else {
    return ExecutionResult.FAILED;
}
```

### Debugging / Running Test

To debug or run the test locally, you will have to use the _Runner_ class from TestProject SDK. All code examples, have JUnit tests that use _Runner_ to debug the automation locally. Debugging or running a test locally with the _Runner_ class, requires authentication before communication with the TestProject Agent \(since it is the execution engine\). Development token for authentication can be easily obtained from the [Developers](https://app.testproject.io/#/developers) page. It should be used as a parameter in one of the _Runner_ factory methods:

**Web**

```text
Runner runner = Runner.createWeb("YOUR_DEV_TOKEN", ...
```

**Android**

```text
Runner runner = Runner.createAndroid("YOUR_DEV_TOKEN", ...
```

**Chrome on Android**

```text
Runner runner = Runner.createAndroidWeb("YOUR_DEV_TOKEN", ...
```

**iOS**

```text
Runner runner = Runner.createIOS("YOUR_DEV_TOKEN", ...
```

**Safari on iOS**

```text
Runner runner = Runner.createIOSWeb("YOUR_DEV_TOKEN", ...
```

**Generic**

```text
Runner runner = Runner.create("YOUR_DEV_TOKEN"...
```

### Using parameters and step reports in your tests

Let's make our example more advanced by adding parameters. To add parameters to your test, you simply need to add fields with relevant annotations.  
 In addition, we will create step reports to separate the different stages of the test \(each report will appear as a separate step in the future execution reports\).

See the relevant platform link for full source code:

* [Web - Extended Test](https://github.com/testproject-io/java-sdk-examples/blob/master/Web/Test/src/main/java/io/testproject/examples/sdk/tests/ExtendedTest.java)
* [Android - Extended Test](https://github.com/testproject-io/java-sdk-examples/blob/master/Android/Test/src/main/java/io/testproject/examples/sdk/tests/ExtendedTest.java)
* [iOS - Extended Test](https://github.com/testproject-io/java-sdk-examples/blob/master/iOS/Test/src/main/java/io/testproject/examples/sdk/tests/ExtendedTest.java)
* [Generic - Extended Test](https://github.com/testproject-io/java-sdk-examples/blob/master/Generic/Test/src/main/java/io/testproject/examples/sdk/tests/ExtendedTest.java)

#### Test Annotations

TestProject SDK provides annotations to describe the test and its parameters:

1. The _**Test**_ annotation is used to better describe the Test and define how it will appear later in TestProject UI:
   * **name** - The name of the test \(if omitted, the name of the class will be used\).
   * **description** - A description of the test which is shown in various places in TestProject platform \(e.g. reporting dashboard\). The description may contain placeholders {{propertyName}} that will be changed dynamically according to test parameters.
   * **version** - A version string which is used for future reference.
2. The _**Parameter**_ annotation is used to better describe your Test inputs and outputs, in the example above there are two inputs - _url_ and _expectedTitle_.
   * **description** - The description of the parameter
   * **direction** - Defines the parameter as an _input_ \(default if omitted\) or an _output_ parameter. An _input_ parameter will receive values when the test is executed while the _output_ parameter value will be retrieved at the end of test execution \(and can be used in following steps later on in the automation scenario\).
   * **defaultValue** - Defines a default value that will be used for the parameter.

#### Reports

Implemented _execute\(\)_ method receives a _Helper_ instance as a parameter.  
 Via this helper, you can obtain an instance of _TestReporter_ class.

```text
TestReporter report = helper.getReporter();
```

Notice the following line in the Extended Test example.  
 This line reports a step based on provided condition and takes a screenshot:

```text
report.step("Profile information saved", profilePage.isSaved(), TakeScreenshotConditionType.Always);
```

Using the following code one can set test result message:

```text
report.result("Test completed successfully");
```

## Addon development

Much like Tests you can develop custom Addons to extend TestProject and shape your automated testing solution for your needs.  
 An Addon is a set of Actions \(one or more\) where each Action does a specific task, a common Addon scenario will be to extend basic set of Actions on complicated UI elements or make wrappers for user defined API.  
 Once created, Actions can be used to design steps of automated tests.

### Addon Manifest

To start developing an Addon a manifest file is required. The manifest is a descriptor of your Addon, it contains a unique GUID for the addon and a list of required permissions.  
 Create an Addon in the [Addons](https://app.testproject.io/#/addons/account) screen and download the generated manifest, placing it in your project resources folder.

### Implement the Addon

Lets review a simple Addon with a **ClearFields** action that clears a form. It can be used on the login form in TestProject Demo website or mobile App:

* [Web - Action](https://github.com/testproject-io/java-sdk-examples/blob/master/Web/Addon/src/main/java/io/testproject/examples/sdk/actions/ClearFieldsAction.java)
* [Android - Action](https://github.com/testproject-io/java-sdk-examples/blob/master/Android/Addon/src/main/java/io/testproject/examples/sdk/actions/ClearFieldsAction.java)
* [iOS - Action](https://github.com/testproject-io/java-sdk-examples/blob/master/iOS/Addon/src/main/java/io/testproject/examples/sdk/actions/ClearFieldsAction.java)

There is also a [Generic](https://github.com/testproject-io/java-sdk-examples/blob/master/Generic/Addon/src/main/java/io/testproject/examples/sdk/actions/AdditionAction.java) action, representing a dummy scenario that can be automated.  
 It can be used as a reference for real scenarios that automate a non-UI \(those hat do not require a Selenium or Appium driver\) actions.

#### Action Class

In order to build an Action that can be executed by TestProject, the class has to implement one of the interfaces that the SDK provides.  
 Action class can also be decorated with the _@Action_ annotation to provide extra information about the action.

Interface implementation requires an implementation of the _execute\(\)_ method, that will be be invoked by the platform to run the Action.  
 The _execute\(\)_ method returns _ExecutionResult_ enum which can be **PASSED** or **FAILED**.

**Web Action**

ClearFields class implements the _WebAction_ interface:

```text
@Action(name = "Clear Fields")
public class ClearFields implements WebAction
```

Action entry point is the _execute_ method:

```text
public ExecutionResult execute(WebAddonHelper helper) throws FailureException
```

Action code searches for visible Forms and then for contained inputs elements, clearing them one by one:

```text
// Get Driver
WebDriver driver = helper.getDriver();

// Search for Form elements
for (WebElement form : driver.findElements(By.tagName("form"))) {

    // Ignore invisible forms
    if (!form.isDisplayed()) {
        continue;
    }

    // Clear all inputs
    for (WebElement element : form.findElements(By.tagName("input"))) {
        element.clear();
    }
}
```

**Android Action**

ClearFields class implements the _AndroidAction_ interface:

```text
@Action(name = "Clear Fields")
public class ClearFields implements AndroidAction
```

Action entry point is the _execute_ method:

```text
public ExecutionResult execute(AndroidAddonHelper helper) throws FailureException
```

Action code searches for EditText elements, clearing them one by one:

```text
for (AndroidElement element : helper.getDriver().findElements(By.className("android.widget.EditText"))) {
    element.clear();
}
```

**iOS Action**

ClearFields class implements the _IOSAction_ interface:

```text
@Action(name = "Clear Fields")
public class ClearFields implements IOSAction
```

Action entry point is the _execute_ method:

```text
public ExecutionResult execute(IOSAddonHelper helper) throws FailureException
```

Action code searches for XCUIElementTypeTextField and XCUIElementTypeSecureTextField elements, clearing them one by one:

```text
for (IOSElement element : helper.getDriver().findElements(By.className("XCUIElementTypeTextField"))) {
    element.clear();
}

for (IOSElement element : helper.getDriver().findElements(By.className("XCUIElementTypeSecureTextField"))) {
    element.clear();
}
```

**Generic Action**

Addition class implements the _GenericAction_ interface:

```text
@Action(name = "Addition", description = "Add {{a}} to {{b}}")
public class Addition implements GenericAction
```

Action entry point is the _execute_ method:

```text
public ExecutionResult execute(AddonHelper helper) throws FailureException
```

Action code performs an addition of values in two variables, assigning result to third:

Actions run in context of a test and assume that required UI state is already in place.  
When the action will be used in a test it will be represented as a single step, usually preceded by other steps.  
However, when debugging it locally, preparations should be done using the _Runner_ class to start from expected UI state:

**Web - State Preparation**

```text
// Create Action
ClearFields action = new ClearFields();

// Prepare state
WebDriver driver = runner.getDriver();
driver.navigate().to("https://example.testproject.io/web/");
driver.findElement(By.id("name")).sendKeys("John Smith");
driver.findElement(By.id("password")).sendKeys("12345");

// Run action
runner.run(action);
```

**Android - State Preparation**

```text
// Create Action
ClearFields action = new ClearFields();

// Prepare state
AndroidDriver driver = runner.getDriver();
driver.findElement(By.id("name")).sendKeys("John Smith");
driver.findElement(By.id("password")).sendKeys("12345");

// Run action
runner.run(action);
```

**iOS - State Preparation**

```text
// Create Action
ClearFields action = new ClearFields();

// Prepare state
IOSDriver driver = runner.getDriver();
driver.findElement(By.id("name")).sendKeys("John Smith");
driver.findElement(By.id("password")).sendKeys("12345");

// Run action
runner.run(action);
```

#### Action Annotations

TestProject SDK provides annotations to describe the action:

1. The _**Action**_ annotation is used to better describe your action and define how it will appear later in TestProject UI:
   * **name** - The name of the action \(if omitted, the name of the class will be used\).
   * **description** - A description of the test which is shown in various places in TestProject platform \(reports for example\). The description can use placeholders {{propertyName}} do dynamically change the text according to test properties.
   * **version** - A version string which is used for future reference.
2. The _**Parameter**_ annotation is used to better describe your action's inputs and outputs, in the example above there are two parameters - _question_ and _answer_.
   * **description** - The description of the parameter
   * **direction** - Defines the parameter as an _input_ \(default if omitted\) or an _output_ parameter. An _input_ parameter will able to receive values when it is being executed while the _output_ parameter value will be retrieved at the end of test execution \(and can be used in other places later on in the automation scenario\).
   * **defaultValue** - Defines a default value that will be used for the parameter.

> NOTE: Unlike tests, actions cannot use assertions because an action is a single generic reusable unit.

### Debugging / Running Actions

To debug or run the action locally, you will have to use the _Runner_ class from TestProject SDK. All code examples, have JUnit tests that use _Runner_ to debug the automation locally.

### Element Actions

Actions can be element based, when their scope is limited to operations on a specific element and not the whole DOM.  
 This allows creating smart crowd based addons for industry common elements and libraries.

_TypeRandomPhone_ is an example of an Element Action:

* [Web - Element Action](https://github.com/testproject-io/java-sdk-examples/blob/master/Web/Addon/src/main/java/io/testproject/examples/sdk/actions/TypeRandomPhoneAction.java)
* [Android - Element Action](https://github.com/testproject-io/java-sdk-examples/blob/master/Android/Addon/src/main/java/io/testproject/examples/sdk/actions/TypeRandomPhoneAction.java)
* [iOS - Element Action](https://github.com/testproject-io/java-sdk-examples/blob/master/iOS/Addon/src/main/java/io/testproject/examples/sdk/actions/TypeRandomPhoneAction.java)

This action generates a random phone number based on provided country code and max digits amount, typing it in a text field:

```text
long number = (long) (Math.random() * Math.pow(10, maxDigits));
phone = String.format("+%s%s", countryCode, number);
element.sendKeys(phone);
return ExecutionResult.PASSED;
```

It also stores the result in an output field \(see the annotation and _**ParameterDirection.OUTPUT**_ configuration\) for further use later in test.  
 When the action is debugged using a Runner, via JUnit test, it's important to pass the element search criteria into the action:

```text
runner.run(action, By.id("phone"));
```

After the Addon is uploaded to TestProject platform this will be done via UI.

#### Element Type

Element Actions are made to be used on a specific Element Types. Element Types are defined in TestProject using XPath to describe target elements similarities:

**Web - Element Type**

It can be a simple definition such as:

```text
//div
```

Or a more complex one, such as:

```text
//div[contains(@class, 'progressbar') and contains(@class, 'widget') and @role = 'progressbar']
```

**Android - Element Type**

It can be a simple definition such as:

```text
//android.widget.Button
```

Or a more complex one, such as:

```text
//android.support.v7.widget.RecyclerView[contains(@resource-id, 'my_view') and .//android.widget.TextView[not(contains(@resource-id, 'average_value'))]]
```

**iOS - Element Type**

It can be a simple definition such as:

```text
//XCUIElementTypeButton
```

Or a more complex one, such as:

```text
//XCUIElementTypeSearchField[contains(@label = 'Categories')]
```

It is up to the Action developer how to narrow and limit the list of element types that the action developed will be applicable to.

## Crowd Code / Addon Proxy

One of the greatest features of the TestProject environment is the ability to execute a code written by someone else.  
 It can be your account colleagues writing actions that you can reuse, or TestProject community users.  
 Developer must download a binary file with the proxy class for the Action he wants to execute.

Assuming your account member uploaded the example Addon, named it _**Example**_ and you want to reuse it's code your Test.  
 To do so, you can download it's proxy JAR and use it like this:

```text
ClearFields clearFieldsAction = ExampleAddon.clearFields();
```

Implemented _execute\(\)_ method receives a _Helper_ instance as a parameter.  
 Via this helper, you can execute the proxy by invoking the _**executeProxy**_ method:

```text
StepExecutionResult result = helper.executeProxy(clearFieldsAction);
```

See examples:

* [Web - Proxy Test](https://github.com/testproject-io/java-sdk-examples/blob/master/Web/Test/src/main/java/io/testproject/examples/sdk/tests/ProxyTest.java)
* [Android - Proxy Test](https://github.com/testproject-io/java-sdk-examples/blob/master/Android/Test/src/main/java/io/testproject/examples/sdk/tests/ProxyTest.java)
* [iOS - Proxy Test](https://github.com/testproject-io/java-sdk-examples/blob/master/iOS/Test/src/main/java/io/testproject/examples/sdk/tests/ProxyTest.java)
* [Generic - Proxy Test](https://github.com/testproject-io/java-sdk-examples/blob/master/Generic/Test/src/main/java/io/testproject/examples/sdk/tests/ProxyTest.java)

## Packaging

In order to upload your Addons or Tests to TestProject, you have to package it as JAR file.  
 Export your code as an uber JAR file with dependencies, excluding TestProject SDK.

See _build.gradle_ or _pom.xml_ files in code examples for details.

## Support

For any further inquiries, please use TestProject support channels:

* [Forum](https://forum.testproject.io/)
* In-app Chat
* Email at support@testproject.io

