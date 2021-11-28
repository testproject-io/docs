---
description: >-
  Use Adaptive Wait to stabilize your tests, Make your test slower or faster
  using Execution speed.
---

# Execution Speed & Adaptive Wait

There are various ways to add waits in your tests. Let's review them and understand each one and their differences.

## **Execution Speed**

Execution speed is an option available for the **entire test **and on **each step** of your test. It should be used for controlling the speed of the tests and not to add fixed pauses in the test. To add dynamic pauses use [Adaptive Wait](https://docs.testproject.io/tips-and-tricks/explicit-wait-and-adaptive-wait#adaptive-wait).

By default, the step pause is happening before the execution of each step and you can choose from "Fast, Normal, Slow, and Very slow" options. You can choose to override the default settings by changing the option to **custom** and choose either **before** or **after** the execution of your test steps. When choosing custom you can also change the pause time manually by typing a preferred number of milliseconds. (1 second = 1000ms)

You can also edit this setting **globally** for each of your test steps by going to the settings of your test and changing the default execution speed.

![](<../.gitbook/assets/image (454).png>)

Here is how you can change **specific step** Execution Speed first, disable "Use Test Default" (inherits from test settings) then choose a custom behavior:

![](<../.gitbook/assets/image (450).png>)



## **Adaptive Wait**

To save you time and improve the stability of your tests, we have developed an adaptive wait that knows when to move to the next action. Now, you can trust your tests without having unnecessary fixed pauses in your tests.

### **Adaptive Wait within the TestProject Smart Recorder**

The adaptive wait functionality is located within **every step **in your test. TestProject will adapt to the actual loading pace of your application and execute the next action **only** when the proper conditions are met. You can set the maximum timeout before the step fails (Set to 15 seconds by default).&#x20;

Unlike a fixed pause, your test will be able to continue even before the time limit if the conditions allow it, therefore increasing the Adaptive wait time can help **stabilize your test** without adding time to the execution.&#x20;

You can edit the Adaptive Wait time **globally** for your test from the test’s settings:

![](<../.gitbook/assets/image (448).png>)



This is how you can change **specific step** Adaptive Wait first, disable "Use Test Default" (inherits from test settings) then choose a custom behavior:

![](<../.gitbook/assets/image (456).png>)



### **How to use Adaptive Wait with the TestProject SDK**

The adaptive wait functionality also appears in the TestProject SDK. You will be able to use it as long as you use the TestProject web/mobile **driver**.

{% tabs %}
{% tab title="Web Example" %}
In the following example, we will navigate to a URL and input a username and password in their respective fields:

```
// This is the test’s execute method, it will contain the actions taken in the test.
  public ExecutionResult execute(WebTestHelper helper) throws FailureException {
// Leverage the TestProject driver.
    WebDriver driver = helper.getDriver();
   // set timeout for adaptive wait driver actions, by increasing this timeout you increase the maximum threshold that the driver will wait for element to become visible.
    driver.setTimeout(15000);
// The TestProject reporter.
    TestReporter report = helper.getReporter();
    By by;
    boolean booleanResult;
    //    Navigates the specified URL.
    booleanResult = driver.testproject().navigateToUrl(ApplicationURL);
    report.step(String.format("Navigate to '%s'",ApplicationURL), booleanResult, TakeScreenshotConditionType.Failure);
    // Type the username.
    by = By.cssSelector("#name");
    booleanResult = driver.testproject().typeText(by,"Username");
    report.step("Type 'Username' in 'name1'", booleanResult, TakeScreenshotConditionType.Failure);
    // Type the password.
    by = By.cssSelector("#password");
    booleanResult = driver.testproject().typeText(by,"12345678");
    report.step("Type '12345678' in 'password1'", booleanResult, TakeScreenshotConditionType.Failure);
// Report the test as passed.
    return ExecutionResult.PASSED;
  }
```
{% endtab %}

{% tab title="Mobile Example" %}
In the following example, we will use the adaptive wait functionality to wait for an Android Element to appear in a coded test, before tapping on it:

```
// This is the test’s execute method, will contain the actions taken in the test.
public ExecutionResult execute(AndroidTestHelper helper) throws FailureException {
   // Leverage the TestProject driver.
    AndroidDriver driver = helper.getDriver();
   // set timeout for adaptive wait driver actions, by increasing this timeout you increase the maximum threshold that the driver will wait for element to become visible.
    driver.setTimeout(15000);
// The TestProject reporter.
    TestReporter report = helper.getReporter();
    By by;
    boolean booleanResult;
    ExecutionResult executionresult;
Then, any action you perform will employ an adaptive wait, for example:
    // Tap on the element by the locator the ID.
    by = By.id("com.google.android.youtube:id/menu_item_1");
    booleanResult = driver.testproject().tap(by);
// Report the step result via the TestProject reporter.
report.step("Tap 'Search1'", booleanResult, TakeScreenshotConditionType.Failure);
// Report the test as passed.
    return ExecutionResult.PASSED;
  }
```
{% endtab %}
{% endtabs %}

### **Advanced Capabilities: “If visible”**

The **“If visible” actions** are:

* Clear contents (if visible)
* Click if visible
* Contains text? (if visible)
* Get text (if visible)
* Long press gesture (if visible)
* Tap (if visible)
* Type text (if visible)

These actions will consider your set adaptive wait time and **only** be executed if the element you have applied them onto appears on the screen. In case that the element does not appear on the screen, the test will continue without failing, showing 100% pass rate, with an indication in the “If visible” action, saying the element never appeared, causing the step not to execute, but pass regardless.

![](../.gitbook/assets/if-visible-action.png)



You can find more details about each one of the actions [here](https://docs.testproject.io/testproject-addons/available-addons/visible-elements-operations-addon#available-actions)**.**

### **Advanced Capabilities: “Is visible”**

The **“Is Visible”** **validations** are:

* Is visible?
* Is invisible?

These validate if the element is visible or invisible on the page or screen and use the adaptive wait mechanism to determine if the step passes or fails.

![](../.gitbook/assets/is-visible-actions.png)

You can find all available validations and more details [here](https://docs.testproject.io/getting-started/available-validations).
