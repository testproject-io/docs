---
description: C# Step-By-Step Test Create using SpecFlow BDD Framework
---

# SpecFlow (C#)

## Briefing

Following this tutorial you will know how to:

* Create your first C# and SpecFlow project.
* Create your first feature
* Use TestProject OpenSDK to write your tests.
* Package & upload your test to TestProject platform.
* Run the test from the website.

## Creating Your First Project

Let's start by creating our first project.

In this tutorial we will use Visual Studio but you can use Visual Studio Code if you prefer. \
You can download both [here](https://visualstudio.microsoft.com).

Before we create our project, we need to install SpecFlow extension for Visual Studio:

* Open the _Extensions_ menu and choose _Manage Extensions_.
* Click _Online_ and search for _SpecFlow_, then install the extension:

![](<../../.gitbook/assets/image (361).png>)

Now let's create our project. First, open the _File_ menu and choose _New -> Project..._:

Next, select the _NUnit Test Project (.NET Core)_ option.&#x20;

> You can also build your tests with xUnit or MSTest, but we will use NUnit in this tutorial.\
>

![](<../../.gitbook/assets/image (351).png>)

Next name your project and press the _Create_ button. In the new window select _NUnit_ as your Test Framework.\


![](<../../.gitbook/assets/image (352).png>)

Now Press _Create_ to finish your project. You will be greeted with the following page structure:\


![](<../../.gitbook/assets/image (337).png>)

Next, let's add TestProject's OpenSDK to the project, so we can write our first test. All you need to do is:

1. Right click your project and select _Manage NuGet Packages..._.
2. Click the _Browse_ tab and search for _testproject opensdk_.
3. You will see 2 dependencies: one for the SDK itself and one for TestProject's SpecFlow plugin. We need to install both.&#x20;

![](<../../.gitbook/assets/image (336) (1) (1).png>)

Congratulations! You are now ready to write your first tests with SpecFlow.

## Write our first test using SpecFlow

SpecFlow is the #1 .NET open-source framework for [Behavior Driven Development](https://specflow.org/bdd/), Acceptance Test Driven Development and Specification by Example. With over 10 million downloads on NuGet, SpecFlow is trusted by teams around the world.

Let's change the existing feature file to one that suits our test. \
We'll rename it to `my-first.feature` and add the following text:

```
Feature: My First Feature
      My first SpecFlow feature using TestProject OpenSDK

Scenario: Login With Different Users
  Given user is on TestProject Demo Login Page
  When user enters <username> and <password>
  And clicks on Login button
  Then user should be logged in succesfully
Examples:
  | username    | password |
  | John Doe    | 12345    |
  | Jane Doe    | 12345    |
```

This feature has one scenario with 4 simple steps. It also has 2 examples; these are translated to a data-driven test.

Now we need to implement those steps. luckily for us, the SpecFlow extension will do some of the work for us:

* Right-click the feature window and select _Generate Step Definitions_.
* You can see the list of steps that will be generated. Just click the _Generate_ button and save the step Definitions in the _Steps_ folder.&#x20;

![](<../../.gitbook/assets/image (355).png>)

Here's what the generated steps look like:

```csharp
using System;
using TechTalk.SpecFlow;

namespace MyFirstSpecFlowProject.Steps
{
    [Binding]
    public class MyFirstFeatureSteps
    {
        [Given(@"user is on TestProject Demo Login Page")]
        public void GivenUserIsOnTestProjectDemoLoginPage()
        {
            ScenarioContext.Current.Pending();
        }

        [When(@"user enters (.*) and (.*)")]
        public void WhenUserEntersAnd(string p0, string p1)
        {
            ScenarioContext.Current.Pending();
        }

        [When(@"clicks on Login button")]
        public void WhenClicksOnLoginButton()
        {
            ScenarioContext.Current.Pending();
        }

        [Then(@"user should be logged in succesfully")]
        public void ThenUserShouldBeLoggedInSuccesfully()
        {
            ScenarioContext.Current.Pending();
        }
    }
}
```

As you can see we have the class attributed as `[Binding]` with all the step methods and their attributes. All we need to do now is implement the steps and our test will be ready!

Let's write a simple test that navigates to TestProject example page and uses the username and password parameters (or `p0` and `p1` as they were generated) to login to the website. \
Here's the code below:

```csharp
using System;
using OpenQA.Selenium;
using OpenQA.Selenium.Support.UI;
using TechTalk.SpecFlow;
using ChromeDriver = TestProject.OpenSDK.Drivers.Web.ChromeDriver;

namespace MyFirstSpecFlowProject.Steps
{
    [Binding]
    public class MyFirstFeatureSteps
    {
        private ChromeDriver driver;

        [BeforeScenario]
        public void CreateDriver()
        {
            driver = new ChromeDriver();
            driver.Manage().Timeouts().ImplicitWait = TimeSpan.FromSeconds(15);
        }

        [Given(@"user is on TestProject Demo Login Page")]
        public void GivenUserIsOnTestProjectDemoLoginPage()
        {
            driver.Navigate().GoToUrl("https://example.testproject.io/web/");
        }

        [When(@"user enters (.*) and (.*)")]
        public void WhenUserEntersUsernameAndPassword(string username, string password)
        {
            driver.FindElement(By.XPath("//input[@id='name']")).SendKeys(username);
            driver.FindElement(By.XPath("//input[@id='password']")).SendKeys(password);
        }

        [When(@"clicks on Login button")]
        public void WhenClicksOnLoginButton()
        {
            driver.FindElement(By.XPath("//button[@id='login']")).Click();
        }

        [Then(@"user should be logged in succesfully")]
        public void ThenUserShouldBeLoggedInSuccesfully()
        {
            new WebDriverWait(driver, TimeSpan.FromSeconds(5)).Until(ExpectedConditions.ElementIsVisible(By.XPath("//button[@id='save']")));
        }

        [AfterScenario]
        public void CloseDriver()
        {
            driver.Quit();
        }
    }
}
```

As you can see we added a few things using TestProject's OpenSDK:

* We added the _CreateDriver()_ method and annotated it with `[BeforeScenario]` , so it will run before all the steps. Here we create a new driver and set the step timeout.
* We added the _CloseDriver()_ method and annotated it with `[AfterScenario]` , so it will run after all the steps and quit the driver. it's a good practice to call `driver.quit()` after all tests.
* Finally, we implemented all the steps using TestProject driver and Selenium's WebDriverWait.

That's all the code we need to write our first test! Now let's make it run.

## Running the Test

To run tests using TestProject's OpenSDK you need to first install and register the TestProject Agent ([download link](https://app.testproject.io/#/download)). You also need a development token which can be obtained [here](https://app.testproject.io/#/integrations/sdk).

You can add the development token to your code, but a better way would be to specify it using an environment variable. To do this we need to add a _.runsettings_ to the project.

The contents of the _.runsettings_ file should be as follows:

```
<RunSettings>
  <RunConfiguration>
    <EnvironmentVariables>
      <!-- List of environment variables we want to set-->
      <TP_DEV_TOKEN>YOUR_DEV_TOKEN</TP_DEV_TOKEN>
    </EnvironmentVariables>
  </RunConfiguration>
</RunSettings>
```

And that's it! Time to run our test. Here's how it's done:

* Make sure your agent is running and registered.
* Open the test explorer by opening the _Test_ menu and selecting the _Test Explorer_ option.
* Press the _Options_ button (rightmost button) and make sure _Configure Run Settings -> Auto Detect runsettings File_ is enabled.
* Choose one of the two scenarios, then press the _Play_ button and watch your test run!

Well done, you just ran your first test! Let's check the report:&#x20;

![](<../../.gitbook/assets/image (365).png>)

As you can see, because we added the _TestProject.OpenSDK.SpecFlowPlugin_ dependency, the test name is reported as the scenario name and the steps are the same as in the feature. Basically, TestProject did all the heavy lifting for us. All that's left to do is upload the test and run it from TestProject platform.

## Package & Upload Tests to TestProject

The next step is to upload our test to the TestProject platform, so we can trigger it remotely from there.

### Package

Before uploading our Test, we should package them into a single ZIP file. Here's how to do it:

* Right-click your solution in the _Solution Explorer_ panel and select _Publish..._

#### First time publishing

If this is your first time publishing, create a new publishing target:

* Choose _Folder_ as your publish target, and press _Next_.&#x20;

![](<../../.gitbook/assets/image (357) (1).png>)

* Choose _Folder_ again, and press _Next_.

![](<../../.gitbook/assets/image (342) (1) (1) (1) (1).png>)

* Change the folder your code is built in to _publish\\_ and press _Finish_.

#### Publish&#x20;

* Press _Publish_ next to the _FolderProfile_ target to create this folder.

![](<../../.gitbook/assets/image (343) (1).png>)

* Right-click your solution in the _Solution Explorer_ panel and select _Open Folder in File Explorer_.
* Zip the newly created `out` folder (right-click the _publish_ folder and select _Send To -> Compressed (Zipped) archive)_

## _Upload_

Now we can upload it to TestProject platform.

In order to upload your test to TestProject, navigate to [http://app.testproject.io](http://app.testproject.io), then click on **New Test** and choose the **Code** option:&#x20;

![](<../../.gitbook/assets/image (358).png>)

Click **next**, upload your ZIP file and create a test package:

![](<../../.gitbook/assets/image (366).png>)

Here you can see a list of all the tests (or test in this case) in your zip file:

![](<../../.gitbook/assets/image (356).png>)

Next, name your test package:

![](<../../.gitbook/assets/image (375).png>)

Now we can execute our test, just click on the play button:

![](<../../.gitbook/assets/image (367).png>)

## Sources

The whole solution and project including demonstrated sources are [available in GitHub](https://github.com/testproject-io/csharp-opensdk).

## Summary

This tutorial taught us four things:

* How to create a C# SpecFlow Project that uses TestProject's OpenSDK.
* How to write features & implement them TestProject OpenSDK driver.
* How to use TestProject's SpecFlow plugin to automatically report the scenario name and steps.
* How to package & upload our tests to TestProject's platform.
