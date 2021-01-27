---
description: Perform Behavior Driven Development with the Java OpenSDK.
---

# Cucumber \(Java\)

The TestProject Java OpenSDK supports automatic reporting of Cucumber features, scenarios and steps using the CucumberReporter plugin in the SDK.

While utilizing the TestProject OpenSDK with Cucumber you will be able to collaborate with your team members in the cloud , share reports, screenshots and automation progress.

Using the plugin will disable the reporting of driver command and automatic reporting of tests.

Instead, it will report:

* A test for every scenario in a feature file
* All steps in a scenario as steps in the corresponding test
* Steps are automatically marked as passed or failed, including the cause of failure.

### Example

If working with IntelliJ as your IDE, it is recommended to install the Gherkin plugin for feature file syntax highlighting and execution.

You can find the plugin through file &gt; settings &gt; plugins:

![IntelliJ Plugin](../../.gitbook/assets/image%20%28275%29.png)

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

![Generate Step Definitions](../../.gitbook/assets/image%20%28277%29.png)

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

![Set Plugin](../../.gitbook/assets/image%20%28270%29.png)

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

![TestProject Report](../../.gitbook/assets/image%20%28273%29.png)

A fully working example can be found in the JavaOpenSDK GitHub documentation [here](https://github.com/testproject-io/java-sdk/tree/master/src/test/java/io/testproject/sdk/tests/examples/frameworks/cucumber).

