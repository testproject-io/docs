# Addon Action Options

## **Action Class**

In order to build an Addon Action that can be executed by TestProject, you need to create a class that implements one of the provided interfaces. The SKD provides the following interfaces:

* WebAction
* AndroidAction
* IOSAction
* GenericAction
* WebElementAction
* AndroidElementAction
* IOSElementAction

In order to use these interfaces you need to create an implementation of the _execute\(\)_ method. This method is what the platform uses when it is running the Action. The _execute\(\)_ method returns _ExecutionResult_ enum which can be **PASSED** or **FAILED**.

Action class can also be decorated with the `@Action` annotation to provide extra information about the action.

All actions run in the context of a test and they assume that the required UI state is already in place.  
When an action is used in a test it is represented as a single step, usually preceded by other steps that setup the UI state.

### Web Action

The web action interface can be used to create an addon that will provide web actions. In order to use it create a class that implements it:

```java
@Action(name="Addon Name")
public class <YourAddonClass> implements WebAction {
...
}
```

Inside this class you need to implement the execute method using the `WebAddonHelper`  

```java
 public ExecutionResult execute(WebAddonHelper helper) throws FailureException {
 ...
 }
```

You can see a full example of an implementation of a WebAction class [here](https://github.com/testproject-io/addons/blob/master/Examples/IOS/src/main/java/io/testproject/examples/sdk/actions/ClearFieldsAction.java) on GitHub. 

### Android Action

The Android action interface is used to create addons that are meant to run on Android devices.

```java
@Action(name = "Addon Name")
public class <YourAndroidAddonClass> implements AndroidAction {
...
}
```

Inside this class you need to implement the execute method using the `AndroidAddonHelper:`

```java
public ExecutionResult execute(AndroidAddonHelper helper) throws FailureException {
...
}
```

You can see a full example of an implementation of an AndroidAction class [here ](https://github.com/testproject-io/addons/blob/master/Examples/Android/src/main/java/io/testproject/examples/sdk/actions/ClearFieldsAction.java)in GitHub.

### iOS Action

The `IOSAction` interface is used to create addons that are meant to run on iOS devices:

```java
@Action(name = "Addon Name")
public class <YouriOSAddonClass> implements IOSAction {
...
}
```

Inside this class you need to implement the execute method using the `IOSAddonHelper:`

```java
public ExecutionResult execute(IOSAddonHelper helper) throws FailureException {
...
}
```

You can see a full example of an implementation of an IOSAddon class [here ](https://github.com/testproject-io/addons/blob/master/Examples/IOS/src/main/java/io/testproject/examples/sdk/actions/ClearFieldsAction.java)in GitHub.

### Generic Action

The `Generic` interface is used to create generic addons:

```java
@Action(name = "Addon Name")
public class <YourAddonClass>implements GenericAction {
...
}
```

Inside this class you need to implement the execute method using the `AddonHelper`

```java
public ExecutionResult execute(AddonHelper helper) throws FailureException {
...
}
```

You can see a full example of an implementation of a GenericAddon class [here ](https://github.com/testproject-io/addons/blob/master/Examples/Generic/src/main/java/io/testproject/examples/sdk/actions/AdditionAction.java)in GitHub.

The generic action can be used for scenarios that automate non-UI actions \(those that do not require a Selenium or Appium driver\).

### Element Actions

Actions can be element based, which means that their scope is limited to operations on a specific element and not the whole DOM.  When using an element action in the recorder, you must specify which element this action will act on. This allows the creation of addons for industry common elements and libraries.

Element Actions may be limited to a particular element by the user selection, or they may be set to only use a specific Element Type. Element Types are defined in TestProject using XPath to describe target element similarities. They can be as simple as you want. For example:

```text
\\div
```

or more complex ones like:

```java
\\div[contains(@class, 'progressbar') and contains(@class, 'widget') and @role = 'progressbar']
```

It is up to the Action developer how to narrow and limit the list of element types that the action developed will be applicable to.

Starting with the Addon SDK 0.65.0, elements need to be located inside the element action using the driver. They can be found simply by using the search criteria provided by the helper object:

```java
element = driver.findElement(helper.getSearchCriteria());
```

#### Web Element Action

The WebElementAction interface can be used to create an addon that will provide web actions that can be appied to specified elements. In order to use it create a class that implements it:

```java
@Action(name="Addon Name")
public class <YourAddonClass> implements WebElementAction {
...
}
```

Inside this class you need to implement the execute method using the `WebAddonHelper` and the `WebElement`

```java
 public ExecutionResult execute(WebAddonHelper helper, WebElement element) throws FailureException {
 ...
 }
```

You can see a full example of an implementation of a WebElementAction class [here ](https://github.com/testproject-io/addons/blob/master/Examples/Web/src/main/java/io/testproject/examples/sdk/actions/TypeRandomPhoneAction.java)on GitHub. Note that you need to apply to the action to the element for Element Actions.

#### Android Element Action

The Android element action interface is used to create addons that are meant to run on specific element on Android devices.

```java
@Action(name = "Addon Name")
public class <YourAndroidAddonClass> implements AndroidElementAction {
...
}
```

Inside this class you need to implement the execute method using the `AndroidAddonHelper`and the `AndroidElement`.

```java
public ExecutionResult execute(AndroidAddonHelper helper, AndroidELement element) throws FailureException {
...
}
```

You can see a full example of an implementation of an AndroidElementAction class [here ](https://github.com/testproject-io/addons/blob/master/Examples/Android/src/main/java/io/testproject/examples/sdk/actions/TypeRandomPhoneAction.java)on GitHub. Note that you need to apply to the action to the element for Element Actions.

#### iOS Element Action

The `IOSElementAction` interface is used to create addons that are meant to run on specific elements on iOS devices:

```java
@Action(name = "Addon Name")
public class <YouriOSAddonClass> implements IOSElementAction {
...
}
```

Inside this class you need to implement the execute method using the `IOSAddonHelper`and the `IOSElement`

```java
public ExecutionResult execute(IOSAddonHelper helper, IOSElement element) throws FailureException {
...
}
```

You can see a full example of an implementation of an IOSElementAddon class [here ](https://github.com/testproject-io/addons/blob/master/Examples/IOS/src/main/java/io/testproject/examples/sdk/actions/TypeRandomPhoneAction.java)on GitHub. Note that you need to apply to the action to the element for Element Actions.

## Addons with Parameters

An addon can perform actions based on inputs you code into it, but sometimes it is helpful to have your addon take in user defined inputs. You can do this with the `@Parameter` annotation.  For example, the following code in your addon class would define two input fields, `countryCode` and `maxDigits` that users could specify when using this addon.

```java
@Parameter
public String countryCode = "1";

@Parameter
public int maxDigits;
```

You can also define output parameters in your addons. Output parameters are a way to store the output of  the actions that your addon does and provide the users of the addon access to that data. They are also defined with the `@Parameter` annotation, but with the **direction** set to `ParameterDirection.OUTPUT`

```java
 @Parameter(direction = ParameterDirection.OUTPUT)
 public String phone;
```

The _**Parameter**_ annotation is used to better describe your action's inputs and outputs. I has the following fields available:

* **description** - \(optional\) The description of the parameter
* **direction** - \(optional\) Defines the parameter as an _input_ \(default if omitted\) or an _output_ parameter. An _input_ parameter will able to receive values when it is being executed while the _output_ parameter value will be retrieved at the end of test execution \(and can be used in other places later on in the automation scenario\).
* **defaultValue** - \(optional\) Defines a default value that will be used for the parameter.

## Debugging Addons Locally

Once you have packaged an addon and uploaded it to TestProject, you will use the TestProject UI to setup the application state to where you can use the addon. However, while you developing the addon locally, you will want to be able to run it without needing to upload it to the TestProject application every time you want to try something out. In order to do this, you need to create a test in your project that will use this action and then setup the state in that test to where the action needs it to be. To do this, you will have to use the  `Runner` class from the TestProject SDK.

For example:

```java
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
        runner.run(new <MyAddonAction>());
    }

    @AfterAll
    public static void tearDown() throws IOException {
        runner.close();
    }
}
```

You also need to ensure that you have setup the state of a webpage so that you action has something to work with. For example, you might create a test in your project that creates an instance of your addon action and then naviages to the TestProject example page and does some ations there.  Once the state has been setup like that you can call the action using the `runner.run(action)` command:

```java
public class Actions {

    public static void runAction(Runner runner) throws Exception {
        // Create Action (replace name with the name of your action)
        <MyAddonAction> action = new <MyAddonAction>();

        // Prepare state
        WebDriver driver = runner.getDriver();
        driver.navigate().to("https://example.testproject.io/web/");
        driver.findElement(By.id("name")).sendKeys("John Smith");
        driver.findElement(By.id("password")).sendKeys("12345");

        // Run action
        runner.run(action);
    }
}
```

Not that if you are using JUnit to create your test you will need to pass in the element search criteria into the action:

```java
runner.run(action, By.id("phone"));
```

## **Action Annotations**

TestProject SDK provides annotations to describe the action. The _**Action**_ annotation is used to better describe your action and define how it will appear later in TestProject UI:

* **name** - \(optional\) The name of the action \(if omitted, the name of the class will be used\).
* **description** - \(optional\) A description of the test which is shown in various places in TestProject platform \(reports for example\). The description can use placeholders {{propertyName}} do dynamically change the text according to test properties.
* **version** - \(optional\) A version string which is used for future reference.

