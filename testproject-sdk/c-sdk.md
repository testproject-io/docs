---
description: 'TestProject SDK for C#'
---

# C\# SDK

[TestProject](https://testproject.io/) is a Free Test Automation platform for Web and Mobile.  
 To get familiar with the TestProject, visit our main [documentation](https://docs.testproject.io/) website.

TestProject SDK is a single, integrated interface to scripting with the most popular open source test automation frameworks.

From now on, you can effortlessly execute Selenium and Appium native tests using a single automation platform that already takes care of all the complex setup, maintenance and configs.

With one unified SDK available across multiple languages, developers and testers receive a go-to toolset, solving some of the greatest challenges in open source test automation.

With TestProject SDK, users save a bunch of time and enjoy the following benefits out of the box:

* Available as a [NuGet](https://www.nuget.org/packages/TestProject.SDK) package.
* 5-mins simple Selenium and Appium setup with a single [Agent](https://docs.testproject.io/testproject-agents) deployment.
* Automatic test reports in HTML/PDF format \(including screenshots\).
* Collaborative reporting dashboards with execution history and RESTful API support.
* Always up-to-date with the latest and stable Selenium driver version.
* A simplified, familiar syntax for both web and mobile applications.
* Complete test runner capabilities for both local and remote executions, anywhere.
* Cross platform support for Mac, Windows, Linux and Docker.
* Ability to store and execute tests locally on any source control tool, such as Git.

## Getting Started

To get started, you need to complete the following prerequisites checklist:

* Login to your account at [https://app.testproject.io/](https://app.testproject.io/) or [register](https://app.testproject.io/signup/) a new one.
* [Download](https://app.testproject.io/#/download) and install an Agent for your operating system or pull a container from [Docker Hub](https://hub.docker.com/r/testproject/agent).
* Run the Agent and [register](https://docs.testproject.io/getting-started/installation-and-setup#register-the-agent) it with your Account.
* Get a development token from [Integrations / SDK](https://app.testproject.io/#/integrations/sdk) page.
* Have [.NET Core SDK 2.1](https://dotnet.microsoft.com/download/dotnet-core/2.1) installed on your machine.
* Have a [Visual Studio](https://visualstudio.microsoft.com/downloads/) IDE installed.

### Installation

TestProject SDK for C\# is available via [NuGet](https://www.nuget.org/packages/TestProject.SDK).

* Right-click the project and select `Manage NuGet Packages...`
* Search for `TestProject SDK` and add it to your project.

## Test Development

A test class has to implement **one** of the following interfaces:

```text
TestProject.SDK.Tests
├── IWebTest
├── IAndroidTest
└── IIOSTest
```

Here is an example of creating & running a test class implementing the `IWebTest` interface.  
 This test performs a login and expects a logout button to appear:

```text
using OpenQA.Selenium;
using TestProject.Common.Attributes;
using TestProject.Common.Enums;
using TestProject.SDK;
using TestProject.SDK.Tests;
using TestProject.SDK.Tests.Helpers;

namespace MyFirstExample
{
	public class Program
	{
		static void Main(string[] args)
		{
			using (Runner runner = new RunnerBuilder("YOUR-DEV-TOKEN")
						.AsWeb(AutomatedBrowserType.Chrome).Build())
			{
				runner.Run(new BasicTest());
			}
		}

		[Test(Name="Basic Test")]
		class BasicTest : IWebTest
		{
			public ExecutionResult Execute(WebTestHelper helper)
			{
				// Get driver initialized by TestProject Agent
				// No need to specify browser type, it can be done later via UI
				var driver = helper.Driver;

				driver.Navigate().GoToUrl("https://example.testproject.io/web/");

				driver.FindElementByCssSelector("#name").SendKeys("John Smith");
				driver.FindElementByCssSelector("#password").SendKeys("12345");
				driver.FindElementByCssSelector("#login").Click();

				if (driver.FindElements(By.CssSelector("#logout")).Count > 0)
					return ExecutionResult.Passed;
				return ExecutionResult.Failed;
			}
		}
	}
}
```

Below are links to other examples with complete source code:

* [Web](https://github.com/testproject-io/csharp-sdk-examples/blob/master/Web/Test/TestProject.SDK.Examples.Web.Test/Test/BasicTest.cs) test executed on [TestProject Demo](https://example.testproject.io/web/index.html) website.
* [Android](https://github.com/testproject-io/csharp-sdk-examples/blob/master/Android/Test/TestProject.SDK.Examples.Android.Test/Test/BasicTest.cs) test executed on [TestProject Demo](https://github.com/testproject-io/android-demo-app) App for Android.
* [iOS](https://github.com/testproject-io/csharp-sdk-examples/blob/master/IOS/Test/Test/BasicTest.cs) test executed on [TestProject Demo](https://github.com/testproject-io/ios-demo-app) App for iOS.

### Test Running

To debug or run the test, you will have to use the **Runner** class.  
 Here' is an `NUnit` example that executes the `BasicTest` shown above:

```text
using NUnit.Framework;
using TestProject.Common.Enums;
using TestProject.SDK.Examples.Web.Runners.Nunit.Base;

namespace TestProject.SDK.Examples.Runners.Nunit
{
	public class BasicTests
	{
		Runner runner;

		[OneTimeSetUp]
        public void SetUp()
        {
            runner = new RunnerBuilder(DevToken).AsWeb(AutomatedBrowserType.Chrome).Build();
        }

		[Test]
		public void TestLogin()
		{
			runner.Run(new BasicTest());
		}

		[OneTimeTearDown]
		public void TearDown()
		{
			runner.Dispose();
		}
	}
}
```

Below are examples for initialization of other Runner types:

**Desktop Web**

```text
var runner = new RunnerBuilder("DEV_TOKEN")
	.AsWeb(AutomatedBrowserType...).Build();
```

**Android**

```text
var runner = new RunnerBuilder("DEV_TOKEN")
	.AsAndroid("DEVICE_UDID", "APP_PACKAGE", "ACTIVITY").Build();
```

**Chrome on Android**

```text
var runner = new RunnerBuilder("DEV_TOKEN")
	.AsAndroidWeb("DEVICE_UDID").Build();
```

**iOS**

```text
var runner = new RunnerBuilder("DEV_TOKEN")
	.AsIOS("DEVICE_UDID", "DEVICE_NAME", "APP_BUNDLE_ID").Build();
```

**Safari on iOS**

```text
var runner = new RunnerBuilder("DEV_TOKEN")
	.AsIOSWeb("IOS_DEVICE_ID", "IOS_DEVICE_NAME").Build();
```

### Reports

TestProject SDK reports all driver commands and their results to the TestProject Cloud.  
 Doing so, allows us to present beautifully designed reports and statistics in our dashboards.

Reports can be completely disabled via `RunnerBuilder`, for example:

```text
var runner = new RunnerBuilder("DEV_TOKEN")
	.WithReportsDisabled()
	.AsWeb(AutomatedBrowserType...)
	.Build();
```

There are more options to disable reporting of specific entities.  
 See [Disabling Reports](https://github.com/testproject-io/csharp-sdk-examples#disabling-reports) section for more information.

### Implicit Project and Job Names

The SDK will attempt to infer Project and Job names from NUnit / MSTest / XUnit attributes.  
 If found, the following logic and priorities take place:

* _Namespace_ of the class where the `Runner` is created, is used for **Project** name.
* _Class_ name where the `Runner` is created, is used for the **Job** name.
* _Test class_ name, or the _Name_ property of the `Test` attribute on the class is used for the **Test** name.

Examples of implicit Project & Job names inferred from annotations:

* [NUnit example](https://github.com/testproject-io/csharp-sdk-examples/blob/master/Web/Test/TestProject.SDK.Examples.Web.Test/Runners/Nunit/DesktopTests.cs)
* [Console Program example](https://github.com/testproject-io/csharp-sdk-examples/blob/master/Web/Test/TestProject.SDK.Examples.Web.Test/Runners/Console/Program.cs)

### Explicit Names

Project and Job names can be also specified explicitly using the relevant options in `RunnerBuilder`, for example:

```text
var runner = new RunnerBuilder("DEV_TOKEN")
	.WithProjectName("My First Project")
	.WithJobName("My First Job")
	.AsWeb(AutomatedBrowserType...)
	.Build();
```

You can specify a Project, a Job name or both. If you don't, the value will be inferred automatically.  
 See [Implicit Project and Job Names](https://github.com/testproject-io/csharp-sdk-examples#implicit-project-and-job-names) section for more information on how these names are inferred.

Examples of explicit Project & Job names configuration:

* [NUnit example](https://github.com/testproject-io/csharp-sdk-examples/blob/master/Web/Test/TestProject.SDK.Examples.Web.Test/Runners/Nunit/ExplicitNameTests.cs)

### Tests Reports

#### Tests Reporting

Tests are reported automatically when a test **ends**, in other works, when `Runner.Run()` method execution ends.  
 Test names are inferred from the `[Test]` attribute's _Name_ property if it is present, or from the test class name.

> This behavior can't be overridden or disabled at this time.

Each call to `Runner.Run` will create a separate test in a job report.  
 Even calls in the same testing framework method behave this way.

For example, following NUnit based code, will generate the following _four_ tests in the report:

```text
		class Test : IWebTest 
		{
			[Parameter]
			public string url;

			public ExecutionResult Execute(WebTestHelper helper)
			{
				helper.Driver.Navigate().GoToUrl(url);
				return ExecutionResult.Passed;
			}
		}

		public DesktopTests(AutomatedBrowserType automatedBrowserType)
		{
			runner = new RunnerBuilder("DevToken")
						.AsWeb(AutomatedBrowserType.Chrome).Build();
		}

		[Test]
		public void RunGoogle()
		{
			var test = new Test() { url = "http://www.google.com" };
			runner.Run(test);
		}

		[Test]
		public void RunTestProject()
		{
			var test = new Test() { url = "http://testproject.io" };
			runner.Run(test);
		}

		[Test]
		public void RunAll()
		{
			var test = new Test() { url = "http://www.google.com" };
			runner.Run(test);
			test = new Test() { url = "http://testproject.io" };
			runner.Run(test);
		}

		[OneTimeTearDown]
		public void TearDown()
		{
			runner.Dispose();
		}
```

Report:

```text
Report
├── RunGoogle
│   └── Navigate To https://google.com/
├── RunTestProject
│   └── Navigate To http://testproject.io
└── RunAll
    ├── Navigate To https://google.com/
    └── Navigate To http://testproject.io
```

#### Steps

Steps are reported automatically when driver commands are executed.  
 Even if this feature is disabled, or in addition, steps can still be reported **manually**

Notice the following line in the [Extended Test](https://github.com/testproject-io/csharp-sdk-examples/blob/master/Web/Test/TestProject.SDK.Examples.Web.Test/Test/ExtendedTest.cs) example.  
 This line reports a step based on provided condition and takes a screenshot:

```text
helper.Reporter.Step("Profile information saved", profilePage.Saved, TakeScreenshotConditionType.Always);
```

Using the following code one can set test result message:

```text
report.Result = "Test completed successfully";
```

### Disabling Reports

Reporting can be disabled during Runner creation.  
 If reporting was explicitly disabled when the runner was created, it can **not** be enabled later.

#### Disable all reports

The following will create a runner with all types of reports disabled \(except manual step reports\):

```text
var runner = new RunnerBuilder("DEV_TOKEN")
	.WithReportsDisabled()
	.Build();
```

#### Disable driver commands reports

Disabling commands reporting will result in test reports with no steps, unless they are reported manually using `helper.Reporter.step()`. The following will disable driver _commands_ reporting:

```text
var runner = new RunnerBuilder("DEV_TOKEN")
	.WithDriverCommandReportingDisabled()
	.Build();
```

## License

TestProject SDK For C\# is licensed under the LICENSE file in the root directory of this source tree.

