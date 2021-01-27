---
description: >-
  How to use TestProject with Behavior Driven Development for the Java, Python
  and C# OpenSDK's.
---

# Using OpenSDK with Behavior Driven Development

## Introduction

Behavior driver development \(BDD\) is a software development process that encourages collaboration among developers, QA and non-technical or business participants in a software project.

It will encourage the teams to use conversations and concrete examples to formalize how an application should behave.

Behavior driven development stems from test driven development \(TDD\) and acceptance driven development \(ATDD\) and offers the following benefits over them:

* More precise guidance on organizing the conversations between developers, QA and business participants.
* Simpler learning curve, being closer to everyday language, especially the given-when-then approach.
* Easy to update as the product changes, plain language is simple to edit and makes changes in automation safer.
* Snowball effect, scenarios become easier and faster to write and automate as more steps definitions are added. Scenarios will likely share common steps, and new scenarios may need nothing more than a different step parameter.

Here we will learn how to incorporate TestProject into your behavior driven development scenarios using each of the TestProject OpenSDK's. 

## Java OpenSDK

The TestProject Java OpenSDK supports automatic reporting of Cucumber features, scenarios and steps using the CucumberReporter plugin in the SDK.

Using the plugin will disable the reporting of driver command and automatic reporting of tests.

Instead, it will report:

* A test for every scenario in a feature file
* All steps in a scenario as steps in the corresponding test
* Steps are automatically marked as passed or failed, including the cause of failure.

### Example

If working with IntelliJ as your IDE, it is recommended to install the Gherkin plugin for feature file syntax highlighting and execution.

You can find the plugin through file &gt; settings &gt; plugins:

![IntelliJ Plugin](../.gitbook/assets/image%20%28275%29.png)

To create your feature files, simply create a file with the .feature extension, it is recommended to store the feature files in a directory for easy access later on.

The feature file will include our Gherkin syntax scenarios and steps, for example:

login\_scenario.feature

```text
Feature: TestProject with Cucumber Framework
  Perform a login scenario with Cucumber

  Scenario: Run a Simple BDD test with TestProject
    Given I navigate to the TestProject example page
    When I perform a login
    Then I should see a logout button
    And I should close the browser

```

Now that you have a feature file created, created the step definitions is necessary.

If you have the plugin installed, you can right click on a step in a feature file, and generate step definitions automatically:

![Generate Step Definitions](../.gitbook/assets/image%20%28277%29.png)

This will give us a step implementations file with methods annotated to match our feature file:

```text
public class MyStepdefs {
    public MyStepdefs() {
        Given("^I navigate to the TestProject example page$", () -> {
        });
        When("^I perform a login$", () -> {
        });
        Then("^I should see a logout button$", () -> {
        });
        And("^I should close the browser$", () -> {
        });
    }
}

```

**You will need to use to initialize a driver from the TestProject OpenSDK to enable the reporting.**

For web and mobile tests you can use any of the available drivers in the SDK or you can use the Generic driver for non-UI tests.

The following is an example of creating a web test through the step implementations with the ChromeDriver from the SDK.

```text
package io.testproject.sdk.tests.examples.frameworks.cucumber.stepdefinitions;

import io.cucumber.java.en.And;
import io.cucumber.java.en.Given;
import io.cucumber.java.en.Then;
import io.cucumber.java.en.When;
import io.testproject.sdk.drivers.web.ChromeDriver;
import org.junit.jupiter.api.Assertions;
import org.openqa.selenium.By;
import org.openqa.selenium.chrome.ChromeOptions;

import java.util.concurrent.TimeUnit;

/**
 * Step definitions for login_scenario.feature.
 */
public class StepDefinitions {

    /**
     * Driver used in this web test.
     */
    private ChromeDriver driver;

    /**
     * Constructs the TestProject driver and navigates to the TestProject
     * example page.
     *
     * @throws Exception if driver initialization fails.
     */
    @Given("I navigate to the TestProject example page")
    public void navigateToPage() throws Exception {
        driver = new ChromeDriver(new ChromeOptions(), "Cucumber", "Login Scenario");
        final int timeout = 1500;
        driver.manage().timeouts().implicitlyWait(timeout, TimeUnit.MILLISECONDS);
        driver.navigate().to("https://example.testproject.io/web/");
    }

    /**
     * Performs a login in the TestProject example page.
     */
    @When("I perform a login")
    public void performLogin() {
        driver.findElement(By.cssSelector("#name")).sendKeys("John Smith");
        driver.findElement(By.cssSelector("#password")).sendKeys("12345");
        driver.findElement(By.cssSelector("#login")).click();    }

    /**
     * Validates if the login was successful by checking if the login button appears.
      */
    @Then("I should see a logout button")
    public void validateLogoutButton() {
        Assertions.assertTrue(driver.findElement(By.cssSelector("#logout")).isDisplayed());
    }

    /**
     * Quits the driver once and closes the session.
     */
    @And("I should close the browser")
    public void closeBrowser() {
        driver.quit();
    }
}

```

The driver will be initialized in our first step implementation.

To run your feature file with the plugin, you can either run the feature files directly from your IDE and specify the plugin in your Run/Debug configuration by specifying the following argument:

```text
 --plugin io.testproject.sdk.internal.reporting.extensions.cucumber.CucumberReporter
```

![Set Plugin](../.gitbook/assets/image%20%28270%29.png)

In addition, you can run the tests via a runner with the @CucumberOptions annotation for JUnit 4 and TestNG.

A runner will look like the following:

```text
package io.testproject.sdk.tests.examples.frameworks.cucumber;

import io.cucumber.junit.Cucumber;
import io.cucumber.junit.CucumberOptions;
import org.junit.AfterClass;
import org.junit.BeforeClass;
import org.junit.runner.RunWith;


@RunWith(Cucumber.class)
@CucumberOptions(features = "src/test/java/io/testproject/sdk/tests/examples/frameworks/cucumber/features/",
        glue = "io.testproject.sdk.tests.examples.frameworks.cucumber.stepdefinitions",
        plugin = "io.testproject.sdk.internal.reporting.extensions.cucumber.CucumberReporter")
public class JUnitTestRunner {

   
    /**
     * Will be executed before the feature files.
     */
    @BeforeClass
    public static void setUp() {
        System.out.println("Starting feature test run");
    }

    /**
     * Will be executed after the feature files.
     */
    @AfterClass
    public static void tearDown() {
        System.out.println("Finishing feature test run");
    }
}

```

Where the TestProject Cucumber reporting plugin is set in the annotation parameters, in general the parameters in the annotation are:

* **features -** Local path to the feature file or directory containing the features.
* **glue -** Package of step implementations.
* **plugins -** Package path of the reporting plugin, in this case it should always be:

  ```text
  io.testproject.sdk.internal.reporting.extensions.cucumber.CucumberReporter
  ```

  To point to the TestProject reporting plugin.

After running the test, your Gherkin syntax will be reported into TestProject:

![TestProject Report](../.gitbook/assets/image%20%28273%29.png)

A fully working example can be found in the JavaOpenSDK GitHub documentation [here](https://github.com/testproject-io/java-sdk/tree/master/src/test/java/io/testproject/sdk/tests/examples/frameworks/cucumber).



## Python OpenSDK

The TestProject Python OpenSDK supports automatic reporting of Behave features, scenarios and steps using the **@behave\_reporter** annotation.

You can install Behave with the following command:

`pip install behave`

Using the annotation will disable the reporting of driver command and automatic reporting of tests.

Instead, it will report:

* A test for every scenario in a feature file
* All steps in a scenario as steps in the corresponding test
* Steps are automatically marked as passed or failed, including the cause of failure.

To enable Behave feature reporting, in your **environment.py** annotate the following methods:

* method used to initialize your driver \(usually, **before\_all**, **before\_feature** or a **fixture**\)
* **after\_step**
* **after\_scenario**

```text
from src.testproject.sdk.drivers import webdriver
from src.testproject.decorator.behave_reporter import behave_reporter


@behave_reporter
before_all(context)
    context.driver = webdriver.Generic(project_name="Python BDD",
     job_name="Behave")


@behave_reporter
after_step:(context, step):
    pass
    

@behave_reporter
after_scenario(context, scenario):
    pass
```

Screenshots by default are only taken on step failure, you can however override this behavior by passing the **screenshot** argument as **True** in your annotation.

```text
@behave_reporter(screenshot=True)
after_step(context, step):
    pass
```

### Example

The following is an example of using TestProject with the Behave framework.

If you are using PyCharm as your IDE, it is recommended to install the Gherkin plugin for feature file syntax highlighting and execution.

The plugin can be found through the file &gt; settings &gt; Plugins section.

![Gherkin Plugin](../.gitbook/assets/image%20%28281%29.png)

After creating a features directory and adding a feature file, these are just files with the .feature extension.

For example:

```text
Feature: TestProject with Behave Framework

  Scenario: Run a Simple BDD test with TestProject
     Given I navigate to the TestProject example page
     When I perform a login
     Then I should see a logout button
```

If you have the plugin installed, you can right click on the definitions in the feature file, and use the context actions to quickly create all the step definition templates for the feature.

![Context Actions](../.gitbook/assets/image%20%28278%29.png)

The following file will be created, and your feature file will know where to search for the step definitions when executed.

```text
from behave import *

use_step_matcher("re")


@given("I navigate to the TestProject example page")
def step_impl(context):
    """
    :type context: behave.runner.Context
    """
    raise NotImplementedError(u'STEP: Given I navigate to the TestProject example page')


@when("I perform a login")
def step_impl(context):
    """
    :type context: behave.runner.Context
    """
    raise NotImplementedError(u'STEP: When I perform a login')


@then("I should see a logout button")
def step_impl(context):
    """
    :type context: behave.runner.Context
    """
    raise NotImplementedError(u'STEP: Then I should see a logout button')
```

In the same features directory, create a file called **environment.py.** 

Behave uses the environment file to define hooks that will be called before or after each step, scenario, feature or even entire test run.

Inside the environment file, create the **after\_step\(context, step\)** and **after\_scenario\(context, scenario\)** methods and annotate them with the **@behave\_reporter** annotation.

{% hint style="info" %}
**Please make sure to also annotate the method used to construct the TestProject driver. Usually the driver is constructed in the environment.py file under a before\_all\(context\), before\_feature\(context, feature\) hooks or before\_tag\(context,**  **tag\) hook using a fixture to guarantee the driver is initialized before the test run.**
{% endhint %}

If you do not want to perform any additional operations after each step or scenario, you can use **pass** in the method.

Example of an **environment.py** file:

```text
from src.testproject.sdk.drivers import webdriver
from src.testproject.decorator.behave_reporter import behave_reporter

""" Executed once per test run: Before any features and scenarios are run.
    Initialize the driver and start the session.
"""


@behave_reporter()
def before_all(context):
    context.driver = webdriver.Chrome(projectname="Python BDD", jobname="Behave")


""" Executed after each step in the scenario.
    Reports the test step.
"""


@behave_reporter(screenshot=True)
def after_step(context, step):
    pass


""" Executed after each scenario in the feature.
    Reports the scenario as a test.
"""


@behave_reporter
def after_scenario(context, scenario):
    pass


""" Executed once per test run: after all features and scenarios are run.
    Quit the driver and close the session.
"""


def after_all(context):
    context.driver.quit()
```

By creating the driver in the **before\_all** hook and storing it in the Behave context, we can use the driver in all other methods using the context after the hook method call, meaning that we have direct access the the driver in all the following hooks, and even our step implementations.

The following will be our step implementations, performing a simple login scenario and validation on Chrome using the TestProject example page:

```text
from behave import *

use_step_matcher("re")


@given('I navigate to the TestProject example page')
def step_impl(context):
    context.driver.get("https://example.testproject.io/web/")


@when('I perform a login')
def step_impl(context):
    context.driver.find_element_by_css_selector("#name").send_keys("John Smith")
    context.driver.find_element_by_css_selector("#password").send_keys("12345")
    context.driver.find_element_by_css_selector("#login").click()


@then('I should see a logout button')
def step_impl(context):
    passed = context.driver.find_element_by_css_selector("#logout").is_displayed()
    assert passed is True
```

The entire project structure should be similar to this:

![Project Structure](../.gitbook/assets/image%20%28276%29.png)

PyCharm Professional allows you to run your Behave via a run configuration setting:

![Run Configuration 1](../.gitbook/assets/image%20%28269%29.png)

![Run configuration 2](../.gitbook/assets/image%20%28272%29.png)

Where the file path specified is the directory containing your feature files.

You can also run the features from the terminal by using the following command:

`behave path/to/features/directory`

The example code is available in the Python OpenSDK GitHub documentation [here](https://github.com/testproject-io/python-sdk/tree/master/tests/examples/frameworks/behave/features).

## C\# OpenSDK

The SDK also supports automatic reporting of SpecFlow features, scenarios and steps through the [TestProject OpenSDK SpecFlow plugin](https://www.nuget.org/packages/TestProject.OpenSDK.SpecFlowPlugin/).

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

![Generate step definitions](../.gitbook/assets/image%20%28280%29.png)

This will display a window where you can select the steps for which to generate step definition methods, as well as the step definition style. 

Click Generate, select the destination for the step definition file and click Save.

![](../.gitbook/assets/image%20%28274%29.png)

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

![](../.gitbook/assets/image%20%28279%29.png)

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

