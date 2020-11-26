---
description: TestProject SDK For Addons
---

# Develop an Addon

[TestProject](https://testproject.io/) is a **Free** Test Automation platform for Web, Mobile and API testing.  
 To get familiar with the TestProject, visit our main [documentation](https://docs.testproject.io/) website.

This document describes the bare minimum steps to start developing **addons** using the Java SDK.

## Addons

Automation building blocks empowering your tests.

An [Addon](https://addons.testproject.io/) is a collection of actions you can use within any [recorded test](https://testproject.io/smart-test-recorder/) to extend the recorder’s capabilities.  
 Addons can be element based or non-UI based:

* Element based Addons provide extended functionalities on customized UI elements.
* Non-UI based Addons combine steps within your recorded tests, such as: File operations, REST API commands, image comparison, etc.

There are hundreds of Addons to choose from, or you can build your own.

Addons are developed in Java and uploaded to the user’s account in a collaborative library.  
 Once uploaded, all team members in the account can use the Addons as part of their tests.

TestProject’s Agent automatically distributes Addons based on the account member’s usage.  
 You can update new versions for Addons, and add more actions or change their functionality according to your needs \(All tests using the newly versioned Addon will be updated as well\).

There are two types of Addons:

1. **Community Addons**: Community Addons are shared by the entire TestProject community and give you the power to effortlessly extend your tests while saving valuable time.
   * The usage of community addon is identical to account addons: Once the community-based action is selected within the [Smart Test Recorder](https://testproject.io/smart-test-recorder/), the Addon is automatically downloaded and installed to the account.
   * Before being shared with the entire community, the TestProject team reviews the code and approves the Addon for public usage.
2. **Account Private Addons**: Account Addons are private and only accessible to account team members. These Addons do not need to be approved by TestProject before the upload/usage.

## Getting Started

To get started, you need to complete the following prerequisites checklist:

* Login to your account at [https://app.testproject.io/](https://app.testproject.io/) or [register](https://app.testproject.io/signup/) a new one.
* [Download](https://app.testproject.io/#/download) and install an Agent for your operating system or pull a container from [Docker Hub](https://hub.docker.com/r/testproject/agent).
* Run the Agent and [register](https://docs.testproject.io/getting-started/installation-and-setup#register-the-agent) it with your Account.
* Get a development token from [Integrations / SDK](https://app.testproject.io/#/integrations/sdk) page.
* Download [Java SDK for Addons](https://app.testproject.io/#/integrations/develop-addon)

### Installation

For a Maven project, add the following to your `pom.xml` file:

```text
<dependency>
    <groupId>io.testprojectgroupId>
    <artifactId>java-sdkartifactId>
    <version>1.0version>
    <systemPath>/path/to/sdk/io.testproject.sdk.java.jarsystemPath>
    <scope>systemscope>
dependency>
```

For a Gradle project, add the following to your `build.gradle` file:

```text
 compile files("/path/to/sdk/io.testproject.sdk.java.jar")
```

Refer to _pom.xml_ and _build.gradle_ files in the provided examples for more details.

### Addon development

An addon is a collection of coded actions you can use within any test.  
 It's all stored in TestProject's collaborative addons library.

#### Addon Manifest

To start developing an Addon a manifest file is required.  
 The manifest is a descriptor of your Addon, it contains a unique GUID for the addon and a list of required permissions.  
 Create an Addon in the [Addons](https://app.testproject.io/#/addons/account) screen and download the generated manifest, placing it in your project resources folder.

#### Implement the Addon

Lets review a simple Addon with a **ClearFields** action that clears a form.  
 It can be used on the login form in TestProject Demo website or mobile App.

```text
package io.testproject.examples.sdk.actions;

import io.testproject.java.annotations.v2.Action;
import io.testproject.java.sdk.v2.addons.WebAction;
import io.testproject.java.sdk.v2.addons.helpers.WebAddonHelper;
import io.testproject.java.sdk.v2.drivers.WebDriver;
import io.testproject.java.sdk.v2.enums.ExecutionResult;
import io.testproject.java.sdk.v2.exceptions.FailureException;
import org.openqa.selenium.By;
import org.openqa.selenium.WebElement;

@Action(name = "Clear Fields")
public class ClearFieldsAction implements WebAction {

    public ExecutionResult execute(WebAddonHelper helper) throws FailureException {

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

        return ExecutionResult.PASSED;
    }
}
```

Below are complete source examples:

* [Web - Action](https://github.com/testproject-io/addons/blob/master/Examples/Web/src/main/java/io/testproject/examples/sdk/actions/ClearFieldsAction.java)
* [Android - Action](https://github.com/testproject-io/addons/blob/master/Examples/Android/src/main/java/io/testproject/examples/sdk/actions/ClearFieldsAction.java)
* [iOS - Action](https://github.com/testproject-io/addons/blob/master/Examples/IOS/src/main/java/io/testproject/examples/sdk/actions/ClearFieldsAction.java)

There is also a [Generic](https://github.com/testproject-io/addons/blob/master/Examples/Generic/src/main/java/io/testproject/examples/sdk/actions/AdditionAction.java) action, representing a dummy scenario that can be automated.  
 It can be used as a reference for real scenarios that automate a non-UI \(those hat do not require a Selenium or Appium driver\) actions.

**Action Class**

In order to build an Action that can be executed by TestProject, the class has to implement one of the interfaces that the SDK provides.  
 Action class can also be decorated with the _@Action_ annotation to provide extra information about the action.

Interface implementation requires an implementation of the _execute\(\)_ method, that will be be invoked by the platform to run the Action.  
 The _execute\(\)_ method returns _ExecutionResult_ enum which can be **PASSED** or **FAILED**.Web Action

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

Android Action

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

iOS Action

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

Generic Action

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
 However, when debugging it locally, preparations should be done using the _Runner_ class to start from expected UI state:Web - State Preparation

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

Android - State Preparation

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

iOS - State Preparation

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

**Action Annotations**

TestProject SDK provides annotations to describe the action:

1. The _**Action**_ annotation is used to better describe your action and define how it will appear later in TestProject UI:
   * **name** - The name of the action \(if omitted, the name of the class will be used\).
   * **description** - A description of the test which is shown in various places in TestProject platform \(reports for example\). The description can use placeholders {{propertyName}} do dynamically change the text according to test properties.
   * **version** - A version string which is used for future reference.
2. The _**Parameter**_ annotation is used to better describe your action's inputs and outputs, in the example above there are two parameters - _question_ and _answer_.
   * **description** - The description of the parameter
   * **direction** - Defines the parameter as an _input_ \(default if omitted\) or an _output_ parameter. An _input_ parameter will able to receive values when it is being executed while the _output_ parameter value will be retrieved at the end of test execution \(and can be used in other places later on in the automation scenario\).
   * **defaultValue** - Defines a default value that will be used for the parameter.

#### Debugging / Running Actions

To debug or run the action locally, you will have to use the _Runner_ class from TestProject SDK.

For example:

```text
package io.testproject.tests.desktop;

import io.testproject.java.enums.AutomatedBrowserType;
import io.testproject.java.sdk.v2.Runner;
import io.testproject.tests.Actions;
import org.junit.jupiter.api.AfterAll;
import org.junit.jupiter.api.BeforeAll;
import org.junit.jupiter.api.Test;

import java.io.IOException;



public class ChromeActions {

    private static Runner runner;

    @BeforeAll
    public static void setup() throws InstantiationException {
        runner = Runner.createWeb("{YOUR_DEV_TOKEN}", AutomatedBrowserType.Chrome);
    }

    @Test
    public void runAction() throws Exception {
        runner.run(new ClearFields());
    }

    @AfterAll
    public static void tearDown() throws IOException {
        runner.close();
    }
}
```

#### Element Actions

Actions can be element based, when their scope is limited to operations on a specific element and not the whole DOM.  
 This allows creating smart crowd based addons for industry common elements and libraries.

_TypeRandomPhone_ is an example of an Element Action:

* [Web - Element Action](https://github.com/testproject-io/addons/blob/master/Examples/Web/src/main/java/io/testproject/examples/sdk/actions/TypeRandomPhoneAction.java)
* [Android - Element Action](https://github.com/testproject-io/addons/blob/master/Examples/Android/src/main/java/io/testproject/examples/sdk/actions/TypeRandomPhoneAction.java)
* [iOS - Element Action](https://github.com/testproject-io/addons/blob/master/Examples/IOS/src/main/java/io/testproject/examples/sdk/actions/TypeRandomPhoneAction.java)

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

**Element Type**

Element Actions are made to be used on a specific Element Types. Element Types are defined in TestProject using XPath to describe target elements similarities:Web - Element Type

It can be a simple definitions such as:

Or a more complex one, such as:

```text
//div[contains(@class, 'progressbar') and contains(@class, 'widget') and @role = 'progressbar']
```

Android - Element Type

It can be a simple definitions such as:

Or a more complex one, such as:

```text
//android.support.v7.widget.RecyclerView[contains(@resource-id, 'my_view') and .//android.widget.TextView[not(contains(@resource-id, 'average_value'))]]
```

iOS - Element Type

It can be a simple definitions such as:

Or a more complex one, such as:

```text
//XCUIElementTypeSearchField[contains(@label = 'Categories')]
```

It is up to the Action developer how to narrow and limit the list of element types that the action developed will be applicable to.

### Packaging

In order to upload your Addons or Tests to TestProject, you have to package it as JAR file.  
 Export your code as an uber JAR file with dependencies, excluding TestProject SDK.

You can use the following build.gradle file to package your addons, just update the **TP\_SDK** variable to the correct location of the TestProject SDK on your system.

```text
group 'io.testproject'
version '1.0.1'

apply plugin: 'java'

// Update the location of TestProject SDK JAR file
def TP_SDK = "__PATH_TO_LOCAL_JAR__/io.testproject.sdk.java.jar"

compileJava.options.encoding = 'UTF-8'

sourceCompatibility = 1.8

repositories {
    mavenCentral()
}

// Configurations
configurations {
    tpsdk
    compile.extendsFrom tpsdk
}

// JAR Task
jar {
    assert file("${TP_SDK}").exists() : "TestProject SDK JAR file was not found, please update the TP_SDK variable"
    archiveName "${rootProject.name}-${version}.jar"
    dependsOn configurations.runtime
    from {
        // Removes TestProject SDK from the final jar file
        (configurations.runtime - configurations.tpsdk).collect {
            it.isDirectory() ? it : zipTree(it)
        }
    }

    // Extract SDK version
    from {
        (configurations.tpsdk).collect {
            zipTree(it).matching {
                include 'testproject-sdk.properties'
            }
        }
    }
}

dependencies {
    tpsdk files("${TP_SDK}")
}
```

See more _build.gradle_ or _pom.xml_ files in code examples for details.

## License

TestProject Addons SDK For Java is licensed under the LICENSE file in the root directory of this source tree.

