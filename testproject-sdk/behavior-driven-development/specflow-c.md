---
description: 'Perform Behavior Driven Development with the C# OpenSDK.'
---

# SpecFlow \(C\#\)

The SDK also supports automatic reporting of SpecFlow features, scenarios and steps through the [TestProject OpenSDK SpecFlow plugin](https://www.nuget.org/packages/TestProject.OpenSDK.SpecFlowPlugin/).

While utilizing the TestProject OpenSDK with SpecFlow you will be able to collaborate with your team members in the cloud , share reports, screenshots and automation progress.

After installing the plugin package using NuGet, SpecFlow-based scenarios that use an SDK driver will be automatically reported to TestProject Cloud.

When the plugin detects that SpecFlow is used, it will disable the reporting of driver command and automatic reporting of tests.

Instead, it will report:

* A separate job for every feature file
* A test for every scenario in a feature file
* All steps in a scenario as steps in the corresponding test

Steps are automatically marked as passed or failed, and Scenario Outlines are supported to create comprehensive living documentation from your specifications on TestProject Cloud.

### Example

It's a good idea to install the SpecFlow Extension for Visual Studio. 

This Extension  provides syntax highlighting for more efficient writing of features files and scenarios.

Installing the extension from within Visual Studio can be done through the Extensions &gt; Manage Extensions menu option \(Visual Studio 2019\) or through Tools &gt; Extensions and Updates \(earlier Visual Studio versions\).

Switch to the Online section, do a search for ‘SpecFlow’ and install the ‘SpecFlow for Visual Studio’ extension.

![Install the SpecFlow Extension for Visual Studio](https://blog.testproject.io/wp-content/uploads/2019/07/specflow_extension_installation.png)

If you’re using SpecFlow 3 \(as we are going to do in this article\), you will also need to disable the SpecFlowSingleFileGenerator custom tool. This can be done through Tools &gt; Options &gt; SpecFlow. Locate the Enable SpecFlowSingleFileGenerator CustomTool option and set it to False.

![Disable the SpecFlowSingleFileGenerator custom tool](https://blog.testproject.io/wp-content/uploads/2019/07/specflow_disable_custom_tool.png)

In this example, a project of the type **‘Class library \(.NET Framework\)’** will be used, because as the code is written again that framework.

After you created the project, add the following packages using the NuGet package manager:

* **SpecFlow.NUnit** – This installs both SpecFlow itself and the NUnit testing framework, which is the unit testing framework we’ll use in this example. Similar packages are available for other unit testing frameworks.
* **NUnit3TestAdapter** – This package allows us to run NUnit-based tests from within Visual Studio.
* **SpecFlow.Tools.MsBuild.Generation** – This package generates code that SpecFlow uses to run feature files \(instead of the legacy SpecFlowSingleFileGenerator custom tool we disabled earlier\).

Now that you have set up your IDE, created a new project and added the required packages, you’re ready to go and create your first SpecFlow feature.

A SpecFlow feature is a file with a .feature file extension, describing the intended behavior of a specific component or feature of the application you are going to write tests for. 

Feature files contain one or more scenarios that describe the specifics of the behavior for that feature, often expressed in very concrete examples. 

Here’s an example feature file.

```text
Feature: TestProject with Behave Framework

  Scenario: Run a Simple BDD test with TestProject
     Given I navigate to the TestProject example page
     When I perform a login
     Then I should see a logout button
```

We can add a new feature file to our project by right-clicking the project name and selecting Add &gt; New Item. Since we have installed the SpecFlow extension before, we can now select SpecFlow &gt; SpecFlow Feature File to add a new feature file to our project:

![](https://blog.testproject.io/wp-content/uploads/2019/07/specflow_add_feature_file.png)

Currently, the feature file has no step implementations.

Right-click anywhere in the feature file editor window and select Generate Step Definitions, another useful feature that comes with the SpecFlow Visual Studio extension.

![Generate step definitions](../../.gitbook/assets/image%20%28280%29.png)

This will display a window where you can select the steps for which to generate step definition methods, as well as the step definition style. 

Click Generate, select the destination for the step definition file and click Save.

![](../../.gitbook/assets/image%20%28274%29.png)

A C\# .cs file with the generated step definition methods will now be added to your project. 

Here is the file:

```text
using System;
using TechTalk.SpecFlow;

namespace ConsoleApp1
{
    [Binding]
    public class TestProjectWithBehaveFrameworkSteps
    {
        [Given(@"I navigate to the TestProject example page")]
        public void GivenINavigateToTheTestProjectExamplePage()
        {
            ScenarioContext.Current.Pending();
        }
        
        [When(@"I perform a login")]
        public void WhenIPerformALogin()
        {
            ScenarioContext.Current.Pending();
        }
        
        [Then(@"I should see a logout button")]
        public void ThenIShouldSeeALogoutButton()
        {
            ScenarioContext.Current.Pending();
        }
    }

```

SpecFlow now knows what code is associated with the steps in the scenarios, and therefore knows what code to run when we run the feature.

You can run the tests by simply using the Test Explorer :

![](../../.gitbook/assets/image%20%28279%29.png)

You can also use the TestProject SDK with the plugin to create automated Selenium and Appium tests, as seen in the Chrome Driver login scenario test below.

```text
using NUnit.Framework;
using System;
using TechTalk.SpecFlow;
using TestProject.OpenSDK.Drivers.Web;

namespace ConsoleApp1
{
    using NUnit.Framework;
    using OpenQA.Selenium;
    using TechTalk.SpecFlow;
    using TestProject.OpenSDK.Drivers.Web;

    /// <summary>
    /// This class contains the step definitions corresponding to the steps in the example scenario.
    /// </summary>
    [Binding]
    public class TestProjectBehaveFrameworkSteps
    {
        /// <summary>
        /// The TestProject ChromeDriver instance to be used in this test class.
        /// </summary>
        private ChromeDriver driver;

        /// <summary>
        /// Start a new browser session before each scenario.
        /// </summary>
        [Before]
        public void StartBrowser()
        {
            this.driver = new ChromeDriver();
        }

        /// <summary>
        /// Implementation of the 'Given' step.
        /// </summary>
        /// <param name="firstName">The first name of the user wanting to log in to the TestProject demo application.</param>
        [Given(@"I navigate to the TestProject example page")]
        public void GivenWantsToUseTheTestProjectDemoApplication(string firstName)
        {
            this.driver.Navigate().GoToUrl("https://example.testproject.io");
        }

        /// <summary>
        /// Implementation of the 'When' step.
        /// </summary>
        /// <param name="username">The username to be provided when logging in.</param>
        /// <param name="password">The password to be provided when logging in.</param>
        [When(@"I perform a login")]
        public void WhenTheyLogInWithUserNameAndPassword(string username, string password)
        {
            this.driver.FindElement(By.CssSelector("#name")).SendKeys(username);
            this.driver.FindElement(By.CssSelector("#password")).SendKeys(password);
            this.driver.FindElement(By.CssSelector("#login")).Click();
        }

        /// <summary>
        /// Implementation of the 'Then' step.
        /// </summary>
        [Then(@"I should see a logout button")]
        public void ThenTheyGainAccessToTheSecurePartOfTheApplication()
        {
            Assert.IsTrue(this.driver.FindElement(By.CssSelector("#logout")).Displayed);
        }

        /// <summary>
        /// Close the browser after each scenario.
        /// </summary>
        [After]
        public void CloseBrowser()
        {
            this.driver.Quit();
        }
    }
}

```

A working example project can be found [here](https://github.com/testproject-io/csharp-sdk/tree/main/TestProject.OpenSDK.SpecFlowExamples).

