This repository contains code examples based on TestProject C# SDK.

## Briefing

This document describes the bare minimum steps to start developing tests using the C# .Net Core SDK.\
TestProject provides a unified test automation SDK with support for Android, iOS and Web applications by utilizing the open-source Selenium and Appium frameworks.
TestProject is OS agnostic and can run on Windows, Linux or Mac.
It is a full stack automation framework with capabilities that allow automation test management, remote and local test execution, job scheduling, reporting dashboards, collaboration and more.
TestProject's C# SDK adds several features not present in .Net Core such as Page Object support via PageFactory.

## Minimum Requirements

* In order to develop TestProject C# tests/addons, you must have .Net Core SDK version v2.1 or greater (Can be downloaded [here](https://dotnet.microsoft.com/download/dotnet-core/2.1))
* In order to execute C# tests/addons, you must have .Net Runtime v2.1 or greater (Can be downloaded [here](https://dotnet.microsoft.com/download/dotnet-core/2.1))
* If you are developing with visual studio, you must use Visual Studio 2017 (Can be downloaded [here](https://visualstudio.microsoft.com/downloads/))

## Preparations

To kick-off automation development with TestProject, it is necessary to have an active TestProject account and the TestProject Agent installed.\
TestProject's Agent is a cross-platform desktop application, allowing you to create, debug and execute your test automation locally.
TestProject Agent can be downloaded from [Agents](https://app.testproject.io/#/agents) page.

### Getting C# SDK

You can download TestProject SDK for C# from the [Developers](https://app.testproject.io/#/developers) page and reference it in your project.

## Test Development

The best way to start developing automated tests with TestProject is by reviewing the source code of a basic test that performs a login and updates a profile form, expecting the save to succeed.\
* [Web](Web/Test/TestProject.SDK.Examples.Web.Test/Test/BasicTest.cs) test executed on [TestProject Demo](https://example.testproject.io/web/index.html) website.
* [Android](Android/Test/TestProject.SDK.Examples.Android.Test/Test/BasicTest.cs) test executed on [TestProject Demo](https://github.com/testproject-io/android-demo-app) App for Android.
* [iOS](IOS/Test/Test/BasicTest.cs) test executed on [TestProject Demo](https://github.com/testproject-io/ios-demo-app) App for iOS.

There is also a [Generic](Generic/Test/TestProject.SDK.Examples.Generic.Test/Test/BasicTest.cs) test, representing  a dummy scenario that can be automated.\
It can be used as a reference for real scenarios that automate a non-UI sequences (those that do not require a Selenium or Appium driver).

### Build your first C# Project
To begin, let's create a .Net Core project and add TestProject SDK as a reference:
* Open Visual studio and create a new project
* From the left side select ```Visual C# => .Net Core```. Then, select ```Class Library```
* Once the project has been created, right-click the project and select ```Manage Nuget Packages...```.
* Search for ```TestProject SDK``` and install it in your project.

There we go, now we're all set! Let's see what

### Test Class

In order to build a Test that can be executed by TestProject, the class has to implement on of the interfaces that the SDK provides.\
Interface implementation requires an implementation of the *Execute()* method, that will be be invoked by the platform to run the Test.\
The *Execute()* method returns *ExecutionResult* enum which can be **PASSED** or **FAILED**.

Below are some examples for Test implementation on different platforms:

<details><summary>Web Test</summary>
<p>

BasicTest class implements the *IWebTest* interface:

```csharp
public class BasicTest : IWebTest
```

Test entry point is the *Execute* method:

```csharp
public ExecutionResult Execute(WebTestHelper helper)
```

The following line of code retrieves a driver to automate the browser.

```csharp
// Get driver initialized by TestProject Agent
// No need to specify browser type, it can be done later via UI
var driver = helper.Driver;
```

Following code is used to navigate the browser to the relevant URL.
After it is executed, TestProject Demo page is loaded.

```csharp
// Navigate to TestProject Demo website
driver.Navigate().GoToUrl("https://example.testproject.io/web/");
```

The following code uses the Page Object Model pattern to login in and complete a profile form, saving it:

```csharp
// Initialize the properties of the LoginPage with the driver
var loginPage = new LoginPage();
PageFactory.InitElements(driver, loginPage);

// Login using provided credentials
loginPage.Login(name, password);

// Initialize the properties of the profilePage with the driver
var profilePage = new ProfilePage();
PageFactory.InitElements(driver, profilePage);
            
// Complete profile forms and save it
profilePage.UpdateProfile(country, address, email, phone);
```

The following return statement will assert test result:

```csharp
return profilePage.Saved ? ExecutionResult.Passed : ExecutionResult.Failed;
```

</p>
</details>

<details><summary>Android Test</summary>
<p>

BasicTest class implements the *IAndroidTest* interface:

```csharp
public class BasicTest : IAndroidTest
```

Test entry point is the *Execute* method:

```csharp
public ExecutionResult Execute(AndroidTestHelper helper)
```

The following line of code retrieves a driver to automate the App.

```csharp
// Get driver initialized by TestProject Agent
var driver = helper.Driver;
```

The following code resets the App and uses the Page Object Model pattern to login in and complete a profile form, saving it:

```csharp
driver.ResetApp();

// Login using provided credentials
var loginPage = new LoginPage(driver);
PageFactory.InitElements(driver, loginPage);

// Perform login
loginPage.Login(name, password);

// Complete profile form
var profilePage = new ProfilePage(driver);
PageFactory.InitElements(driver, profilePage);

profilePage.UpdateProfile(country, address, email, phone);
```

The following return statement will assert test result:

```csharp
return profilePage.Saved ? ExecutionResult.Passed : ExecutionResult.Failed;
```

</p>
</details>

<details><summary>iOS Test</summary>
<p>

BasicTest class implements the *IIOSTest* interface:

```csharp
public class BasicTest : IIOSTest
```

Test entry point is the *Execute* method:

```csharp
public ExecutionResult Execute(IOSTestHelper helper)
```

The following line of code retrieves a driver to automate the App.

```csharp
// Get driver initialized by TestProject Agent
var driver = helper.Driver;
```

The following code resets the App and uses the Page Object Model pattern to login in and complete a profile form, saving it:

```csharp
driver.ResetApp();

// Login using provided credentials
var loginPage = new LoginPage(driver);
PageFactory.InitElements(driver, loginPage);

// Perform login
loginPage.Login(name, password);

// Complete profile form
var profilePage = new ProfilePage(driver);
PageFactory.InitElements(driver, profilePage);

profilePage.UpdateProfile(country, address, email, phone);
```

The following return statement will assert test result:

```csharp
return profilePage.Saved ? ExecutionResult.Passed : ExecutionResult.Failed;
```

</p>
</details>

<details><summary>Generic Test</summary>
<p>

BasicTest class implements the *IGenericTest* interface:

```csharp
public class BasicTest : IGenericTest
```

Test entry point is the *execute* method:

```csharp
public ExecutionResult Execute(GenericTestHelper helper)
```

The following code adds the value stored in 'a' variable to the value in 'b' and if equals 2, asserts success:

```csharp
int a = 1, b = 1;

if (a + b == 2)
    return ExecutionResult.Passed;
else
    return ExecutionResult.Failed;

```

</p>
</details>

### Debugging / Running Test

To debug or run the test locally, you will have to use the *Runner* class from TestProject SDK.
All code examples, have NUnit tests that use *Runner* to debug the automation locally.
Debugging or running a test locally with the *Runner* class, requires authentication before communication with the TestProject Agent (since it is the execution engine).
Development token for authentication can be easily obtained from the [Developers](https://app.testproject.io/#/developers) page.
It should be used as a parameter in one of the *Runner* factory methods:

<details><summary>Web</summary>
<p>

```csharp
var runner = RunnerFactory.Instance.CreateWeb("YOUR_DEV_TOKEN", AutomatedBrowserType.Chrome) // Use the BrowserName you need
```

</p>
</details>

<details><summary>Android</summary>
<p>

```csharp
var runner = RunnerFactory.Instance.CreateAndroid("YOUR_DEV_TOKEN", "YOUR_EMULATOR_ID", "YOUR_APP_PACKAGE", "YOUR_ACTIVITY")
```

</p>
</details>

<details><summary>Chrome on Android</summary>
<p>

```csharp
var runner = RunnerFactory.Instance.CreateAndroidWeb("YOUR_DEV_TOKEN", "YOUR_EMULATOR_ID", BrowserName.Chrome) // Use the BrowserName you need
```

</p>
</details>

<details><summary>iOS</summary>
<p>

```csharp
var runner = RunnerFactory.Instance.CreateIOS("YOUR_DEV_TOKEN", "YOUR_IOS_DEVICE_ID", "YOUR_IOS_DEVICE_NAME", "YOUR_IOS_APP")
```

</p>
</details>

<details><summary>Safari on iOS</summary>
<p>

```csharp
var runner = RunnerFactory.Instance.CreateIOSWeb("YOUR_DEV_TOKEN", "YOUR_IOS_DEVICE_ID", "YOUR_IOS_DEVICE_NAME")
```

</p>
</details>

<details><summary>Generic</summary>
<p>

```csharp
var runner = RunnerFactory.Instance.Create("YOUR_DEV_TOKEN")
```

</p>
</details>

### Using parameters and step reports in your tests

Let's make our example more advanced by adding parameters. To add parameters to your test, you simply need to add fields with relevant attributes.\
In addition, we will create step reports to separate the different stages of the test (each report will appear as a separate step in the future execution reports).

See the relevant platform link for full source code:

* [Web - Extended Test](Web/Test/TestProject.SDK.Examples.Web.Test/Test//ExtendedTest.cs)
* [Android - Extended Test](Android/Test/TestProject.SDK.Examples.Android.Test/Test//ExtendedTest.cs)
* [iOS - Extended Test](IOS/Test/Test/ExtendedTest.cs)
* [Generic - Extended Test](Generic/Test/TestProject.SDK.Examples.Generic.Test/Test/ExtendedTest.cs)

#### Test Attributes

TestProject SDK provides attributes to describe the test and its parameters:

 1. The ***Test*** attribute is used to better describe the Test and define how it will appear later in TestProject UI:
    * **Name** - The name of the test (if omitted, the name of the class will be used).
    * **Description** - A short description of the test which is shown in various places in TestProject platform (e.g. reporting dashboard). The description may contain placeholders {{propertyName}} that will be changed dynamically according to test parameters.
    * **Version** - A version string which is used for future reference.
 1. The ***Parameter*** attribute is used to better describe your Test inputs and outputs, in the example above there are two inputs - *url* and *expectedTitle*.
    * **Description** - The description of the parameter
    * **Direction** - Defines the parameter as an *Input* (default if omitted) or an *Output* parameter. An *Input* parameter will receive values when the test is executed while the *Output* parameter value will be retrieved at the end of test execution (and can be used in following steps later on in the automation scenario).
    * **DefaultValue** - Defines a default value that will be used for the parameter.

#### Reports

Implemented *Execute()* method receives a _Helper_ instance as a parameter.\
Via this helper, you can obtain an instance of _TestReporter_ class.

```csharp
var report = helper.Reporter;
```

Notice the following line in the Extended Test example.\
This line reports a step based on provided condition and takes a screenshot:

```csharp
report.Step("Profile information saved", profilePage.Saved, TakeScreenshotConditionType.Always);
```

Using the following code one can set test result message:

```csharp
report.Result = "Test completed successfully";
```

## Addon development

Much like Tests you can develop custom Addons to extend TestProject and shape your automated testing solution for your needs.\
An Addon is a set of Actions (one or more) where each Action does a specific task, a common Addon scenario will be to extend basic set of Actions on complicated UI elements or make wrappers for user defined API.\
Once created, Actions can be used to design steps of automated tests.

### Addon Manifest

To start developing an Addon a manifest file is required. The manifest is a descriptor of your Addon, it contains a unique GUID for the addon and a list of required permissions.\
Create an Addon in the [Addons](https://app.testproject.io/#/addons/account) screen and download the generated manifest. Then, add the manifest to your package as follows:
* If your addon consists of a single file (e.g. has no dependencies), add the manifest to your project root folder. Then, mark it as an embedded resource by opening the *Properties* panel and change *Build Action* to *Embedded Resource*.
* If your addon consists of multiple files (e.g. has dependencies), add the manifest to the .zip file that you are going to upload to TestProject.

### Implement the Addon

Lets review a simple Addon with a **ClearFields** action that clears a form.
It can be used on the login form in TestProject Demo website or mobile App:

* [Web - Action](Web/Addon/TestProject.SDK.Examples.Web.Addon/Addon/ClearFieldsAction.cs)
* [Android - Action](Android/Addon/TestProject.SDK.Examples.Android.Addon/Addon/ClearFieldsAction.cs)
* [iOS - Action](IOS/Addon/TestProject.SDK.Examples.IOS.Addon/Addon/ClearFieldsAction.cs)

There is also a [Generic](Generic/Addon/TestProject.SDK.Examples.Generic.Addon/Addon/AdditionAction.cs) action, representing  a dummy scenario that can be automated.\
It can be used as a reference for real scenarios that automate a non-UI (those hat do not require a Selenium or Appium driver) actions.

#### Action Class

In order to build an Action that can be executed by TestProject, the class has to implement one of the interfaces that the SDK provides.\
Action class can also be decorated with the *[Action]* attribute to provide extra information about the action.

Interface implementation requires an implementation of the *Execute()* method, that will be be invoked by the platform to run the Action.\
The *Execute()* method returns *ExecutionResult* enum which can be **PASSED** or **FAILED**.

<details><summary>Web Action</summary>
<p>

```csharp
[Action(Name = "Clear Fields")]
public class ClearFieldsAction : IWebAction
```

Action entry point is the *Execute* method:

```csharp
public ExecutionResult Execute(WebAddonHelper helper)
```

Action code searches for visible Forms and then for contained inputs elements, clearing them one by one:

```csharp
// Get Driver
var driver = helper.Driver;

// Search for Form elements
foreach (IWebElement form in driver.FindElements(By.TagName("form")))
{
    // Ignore invisible forms
    if (!form.Displayed)
        continue;

    // Clear all inputs
    foreach (IWebElement element in form.FindElements(By.TagName("input")))
        element.Clear();
}

return ExecutionResult.Passed;
```

</p>
</details>

<details><summary>Android Action</summary>
<p>

```csharp
[Action(Name = "Clear Fields")]
public class ClearFieldsAction : IAndroidAction
```

Action entry point is the *Execute* method:

```csharp
public ExecutionResult Execute(AndroidAddonHelper helper)
```

Action code searches for EditText elements, clearing them one by one:

```csharp
foreach (AndroidElement element in helper.Driver.FindElements(By.ClassName("android.widget.EditText")))
    element.Clear();
```

</p>
</details>

<details><summary>iOS Action</summary>
<p>

```csharp
@Action(name = "Clear Fields")
public class ClearFields : IIOSAction
```

Action entry point is the *Execute* method:

```csharp
public ExecutionResult Execute(IOSAddonHelper helper)
```

Action code searches for XCUIElementTypeTextField and XCUIElementTypeSecureTextField elements, clearing them one by one:

```csharp
for (var element in helper.Driver.findElements(By.className("XCUIElementTypeTextField")))
    element.clear();

for (IOSElement element : helper.Driver.findElements(By.className("XCUIElementTypeSecureTextField")))
    element.clear();
```

</p>
</details>

<details><summary>Generic Action</summary>
<p>

```csharp
[Action(Name = "Addition", Description = "Add {{a}} to {{b}}")]
public class AdditionAction : IGenericAction
```

Action entry point is the *Execute* method:

```csharp
public ExecutionResult Execute(GenericAddonHelper helper)
```

Action code performs an addition of values in two variables, assigning result to third:

```csharp
result = a + b;
```

</p>
</details>


Actions run in context of a test and assume that required UI state is already in place.\
When the action will be used in a test it will be represented as a single step, usually preceded by other steps.\
However, when debugging it locally, preparations should be done using the *Runner* class to start from expected UI state:

<details><summary>Web - State Preparation</summary>
<p>

```csharp
// Create Action
ClearFields action = new ClearFields();

// Prepare state
var driver = (WebDriver)runner.GetDriver();
driver.Navigate().GoToUrl("https://example.testproject.io/web/");
driver.FindElement(By.Id("name")).SendKeys("John Smith");
driver.FindElement(By.Id("password")).SendKeys("12345");

// Run action
runner.Run(action);
```

</p>
</details>

<details><summary>Android - State Preparation</summary>
<p>

```csharp
// Create Action
var action = new ClearFields();

// Prepare state
var driver = (AndroidDriver)runner.GetDriver();
driver.FindElement(By.Id("name")).SendKeys("John Smith");
driver.FindElement(By.Id("password")).SendKeys("12345");

// Run action
runner.Run(action);
```

</p>
</details>

<details><summary>iOS - State Preparation</summary>
<p>

```csharp
// Create Action
var action = new ClearFields();

// Prepare state
var driver = (IOSDriver)runner.GetDriver();
driver.FindElement(By.Id("name")).SendKeys("John Smith");
driver.FindElement(By.Id("password")).SendKeys("12345");

// Run action
runner.Run(action);
```

</p>
</details>

#### Action Attributes

TestProject SDK provides attributes to describe the action:

 1. The ***Action*** attribute is used to better describe your action and define how it will appear later in TestProject UI:
    * **Name** - The name of the action (if omitted, the name of the class will be used).
    * **Description** - A description of the test which is shown in various places in TestProject platform (reports for example). The description can use placeholders {{propertyName}} do dynamically change the text according to test properties.
    * **Version** - A version string which is used for future reference.
 1. The ***Parameter*** attribute is used to better describe your action's inputs and outputs, in the example above there are two parameters - *question* and *answer*.
    * **Description** - The description of the parameter
    * **Direction** - Defines the parameter as an *input* (default if omitted) or an *output* parameter. An *input* parameter will able to receive values when it is being executed while the *output* parameter value will be retrieved at the end of test execution (and can be used in other places later on in the automation scenario).
    * **DefaultValue** - Defines a default value that will be used for the parameter.

> NOTE: Unlike tests, actions cannot use assertions because an action is a single generic reusable unit.

### Debugging / Running Actions

To debug or run the action locally, you will have to use the *Runner* class from TestProject SDK.
All code examples, have NUnit tests that use *Runner* to debug the automation locally.

### Element Actions

Actions can be element based, when their scope is limited to operations on a specific element and not the whole DOM.\
This allows creating smart crowd based addons for industry common elements and libraries.

*TypeRandomPhone* is an example of an Element Action:

* [Web - Element Action](Web/Addon/TestProject.SDK.Examples.Web.Addon/Addon/TypeRandomPhoneAction.cs)
* [Android - Element Action](Android/Addon/TestProject.SDK.Examples.Android.Addon/Addon/TypeRandomPhoneAction.cs)
* [iOS - Element Action](IOS/Addon/TestProject.SDK.Examples.IOS.Addon/Addon/TypeRandomPhoneAction.cs)

This action generates a random phone number based on provided country code and max digits amount, typing it in a text field:

```csharp
var randomer = new Random();
long number = randomer.Next(1, (int)Math.Pow(10, maxDigits));
phone = $"+{countryCode}{number}";
element.SendKeys(phone);
return ExecutionResult.Passed;
```

It also stores the result in an output field (see the attribute and ***ParameterDirection.OUTPUT*** configuration) for further use later in test.\
When the action is debugged using a Runner via NUnit test, it's important to pass the element search criteria into the action:

```csharp
runner.Run(action, By.Id("phone"));
```

After the Addon is uploaded to TestProject platform this will be done via UI.

#### Element Type

Element Actions are made to be used on a specific Element Types.
Element Types are defined in TestProject using XPath to describe target elements similarities:

<details><summary>Web - Element Type</summary>
<p>

It can be a simple definitions such as:

```xml
//div
```

Or a more complex one, such as:

```xml
//div[contains(@class, 'progressbar') and contains(@class, 'widget') and @role = 'progressbar']
```

</p></details>

<details><summary>Android - Element Type</summary>
<p>

It can be a simple definitions such as:

```xml
//android.widget.Button
```

Or a more complex one, such as:

```xml
//android.support.v7.widget.RecyclerView[contains(@resource-id, 'my_view') and .//android.widget.TextView[not(contains(@resource-id, 'average_value'))]]
```

</p></details>

<details><summary>iOS - Element Type</summary>
<p>

It can be a simple definitions such as:

```xml
//XCUIElementTypeButton
```

Or a more complex one, such as:

```xml
//XCUIElementTypeSearchField[contains(@label = 'Categories')]
```

</p></details>

It is up to the Action developer how to narrow and limit the list of element types that the action developed will be applicable to.

## Crowd Code / Addon Proxy

One of the greatest features of the TestProject environment is the ability to execute a code written by someone else.\
It can be your account colleagues writing actions that you can reuse, or TestProject community users.\
Developer must download a binary file with the proxy class for the Action he wants to execute.

Assuming your account member uploaded the example Addon, named it ***Example Addon*** and you want to reuse it's code your Test.\
To do so, you can download it's proxy DLL and use it like this:

```csharp
var clearFieldsAction = ExampleAddon.CreateClearFieldsAction();
```

Implemented *Execute()* method receives a _Helper_ instance as a parameter.\
Via this helper, you can execute the proxy by invoking the ***ExecuteProxy*** method:

```csharp
StepExecutionResult result = helper.ExecuteProxy(clearFieldsAction);
```

See examples:

* [Web - Proxy Test](Web/Test/TestProject.SDK.Examples.Web.Tests/Tests/ProxyTest.cs)
* [Android - Proxy Test](Android/Test/TestProject.SDK.Examples.Android.Tests/Tests/ProxyTest.cs)
* [iOS - Proxy Test](IOS/Test/TestProject.SDK.Examples.IOS.Tests/Tests/ProxyTest.cs)
* [Generic - Proxy Test](Generic/Test/TestProject.SDK.Examples.Generic.Tests/Tests/ProxyTest.cs)

## Packaging


In order to upload your Addons or Tests to TestProject you must prepare either a *DLL* file or a *ZIP* file:\
* If your package only depends on TestProject SDK, you can upload the built *DLL* file to TestProject UI.
* If your package has other dependencies (e.g. DropBox API), Create a zip file from your project output (including dependencies, excluding TestProject SDK) and upload it to TestProject UI.

Here's a simple example based on our [Web - Proxy Test](Web/Test/TestProject.SDK.Examples.Web.Tests/Tests/ProxyTest.cs) Example\
To upload this test we will have to create a *ZIP* file containing 2 *DLL* files:
* TestProject.SDK.Examples.Web.Tests.dll - This is the project output.
* AddonProxy.dll - the addon proxy this test uses.


We are currently working on tools to make deployment easier for you. Stay tuned!

## Support

For any further inquiries, please use TestProject support channels:

* [Forum](https://forum.testproject.io/index.php/board,11.0.html)
* [Help Desk](https://support.testproject.io/)
