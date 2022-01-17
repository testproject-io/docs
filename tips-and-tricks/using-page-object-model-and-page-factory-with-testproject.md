# Using Page object model and Page Factory with TestProject

Test automation is an important part of any software testing project, but effective test automation needs to be thought through and designed well. There are several strategies and methods that can be used to keep your test automation efficient and easy to run and maintain over time. A couple of common strategies for this include the page object and page factory models. These approaches to test automation allow you to keep the tests modular and well organized for maximum effectiveness. These strategies are most often used in coded tests and TestProject supports them in any coded tests you make or run in the platform, but the same concepts can also be used within the Test Recorder as well.

## Page Object in Recorded Tests

The page object model is essentially a way of organizing your tests so that you have one class per page and that class contains the elements for that page along with the methods for acting on those elements. A similar concept can be applied within the Recorder. For example, you could create a test for logging into your app. You can then use that test in all other tests in the project that need to start with logging in.&#x20;

To do that in the Recorder, just click "add a new test as a step" and select the test. (In our case the login test):

![](<../.gitbook/assets/image (461) (2).png>)

You can then choose the login test as a test step in your current test case.&#x20;

![](<../.gitbook/assets/image (453) (1).png>)

This lets you re-use the same login test in multiple tests which means that if something changes on the login page, you only need to update that one test, and all of the tests using it will get that change.

## Page Object in Coded Tests

The Page object model is of course well suited to coded tests. This section will walk you through an example of how you can use the page object model in an android test **** written in Java.

### **Build your First Test with Appium**

Let’s start by learning how to create a “plain” Appium automated test for Android. The code below automates the TestProject Demo app. You can download its [APK](https://github.com/testproject-io/android-demo-app/tree/master/APK) or view the [complete source code](https://github.com/testproject-io/android-demo-app).

To start the automation, the test prepares Android driver capabilities with all the required information about the device under test (DUT) and App under test (AUT). Then, using these capabilities, it initiates the Android driver that will be used to invoke various Appium actions on the mobile application. To perform the actions, Appium must identify the elements it interacts with. To do so, it uses various location strategies.

The most convenient location strategy is the ID (aka. resource-id in Android). For example, it searches for the login button to make sure that the login screen is displayed using _By.id_ and the value _login._ I will show how to identify your element locators later in this tutorial, [here](https://blog.testproject.io/2018/07/14/page-object-model-appium-java-android/#ElementLocator).

**Basic Login Test:**&#x20;

```java
package io.testproject.appium.tests;

import io.appium.java_client.android.AndroidDriver;
import io.appium.java_client.android.AndroidKeyCode;
import io.appium.java_client.remote.AndroidMobileCapabilityType;
import io.appium.java_client.remote.MobileCapabilityType;
import org.openqa.selenium.By;
import org.openqa.selenium.Platform;
import org.openqa.selenium.remote.DesiredCapabilities;

import java.net.URL;

public class PositiveLoginTest {

 private final static String APP_PACKAGE_NAME = "io.testproject.demo";
 private final static String APP_ACTIVITY_NAME = ".MainActivity";
 private final static String PASSWORD = "12345";

 public static void main(String[] args) throws Exception {

 // Prepare Appium session
 DesiredCapabilities capabilities = DesiredCapabilities.android();
 capabilities.setCapability(MobileCapabilityType.PLATFORM_NAME, Platform.ANDROID);
 capabilities.setCapability(MobileCapabilityType.UDID, "YOUR_DEVICE_UDID");
 capabilities.setCapability(MobileCapabilityType.NO_RESET, false);
 capabilities.setCapability(AndroidMobileCapabilityType.APP_PACKAGE, APP_PACKAGE_NAME);
 capabilities.setCapability(AndroidMobileCapabilityType.APP_ACTIVITY, APP_ACTIVITY_NAME);

 // Initialize driver
 AndroidDriver driver = new AndroidDriver(new URL("http://0.0.0.0:4723/wd/hub"), capabilities);

 // Discard state
 driver.resetApp();

 // Will throw exception if login element missing
 driver.findElement(By.id("login"));

 // Hide keyboard if visible
 if (driver.findElements(By.className("UIAKeyboard")).size() != 0) {
 driver.pressKey(new KeyEvent(AndroidKey.ESCAPE));
 }

 // Type Full Name
 driver.findElement(By.id("name")).sendKeys("John Smith");

 // Type Password
 driver.findElement(By.id("password")).sendKeys(PASSWORD);

 // Click Login
 driver.findElement(By.id("login")).click();

 // Verify login
 if (driver.findElement(By.id("greetings")).isDisplayed()) {
 System.out.println("Test completed successfully");
 }

 // Close session
 driver.quit();
 }
}
```

### **Page Object Model and Page Factory Advantages vs. “Plain” Appium**

This demonstrates how to create a “Plain” Appium test, but let's see how we can improve it with the Page Object Model (POM). Below are the advantages of utilizing POM as opposed to “plain” Appium:

| **“Plain” Appium**               | **POM Appium**                                           |
| -------------------------------- | -------------------------------------------------------- |
| Mix of test logic and UI actions | Separation of duties to OOP classes                      |
| Coupled design                   | Decoupling objects library from decision taking in tests |
| Difficult maintenance            | One authority to manage page elements and UI action      |
| Code redundancy                  | No duplicate findElement calls and UI manipulations      |
| Unnecessary complexity           | Self-explanatory code, thanks to FindBy annotations      |

### **Create Page Classes by Utilizing Page Object and Page Factory**

In order to create the page object model, you will need to define the page classes. In the [demo application](https://blog.testproject.io/2018/07/14/page-object-model-appium-java-android/#DemoApp) there are two pages: the Login page and the Profile page.

To map the elements, POM uses the FindBy annotations. These annotations should be used to decorate the fields declared for the elements. Location strategies can be different, but the most convenient one is the ID (aka. resource-id in Android).

While creating tests like this it can be helpful to use the [inspector ](../using-the-smart-test-recorder/finding-and-using-elements/element-inspector.md)and [element locator](../using-the-smart-test-recorder/finding-and-using-elements/element-locator.md) in order to find the correct values.

![](https://blog.testproject.io/wp-content/uploads/2018/07/Android-Element-Locator-512x469.png)

These values can then be placed in the annotations in the code. Then, initElements method residing on the PageObject factory class should be invoked to initialize all the elements of the page.

Elements, page class fields, are now being used across the page to manipulate the UI and encapsulated in methods invoked externally.

**Login Page Class**:

```java
package io.testproject.appium.pom.tests.pages;

import io.appium.java_client.android.AndroidDriver;
import io.appium.java_client.android.AndroidElement;
import io.appium.java_client.pagefactory.AndroidFindBy;
import io.appium.java_client.pagefactory.AppiumFieldDecorator;
import org.openqa.selenium.support.PageFactory;

import java.time.Duration;

public class LoginPage {

    private AndroidDriver<AndroidElement> driver;

    public LoginPage() {
    }

    public LoginPage(AndroidDriver<AndroidElement> driver) {
        this.driver = driver;
        PageFactory.initElements(new AppiumFieldDecorator(driver, Duration.ofSeconds(5)), this);
    }

    @AndroidFindBy(className = "UIAKeyboard")
    private AndroidElement keyboard;

    @AndroidFindBy(id = "name")
    private AndroidElement nameElement;

    @AndroidFindBy(id = "password")
    private AndroidElement passwordElement;

    @AndroidFindBy(id = "login")
    private AndroidElement loginElement;

    public boolean isDisplayed() {
        return loginElement.isDisplayed();
    }

    public void typeName(String name) {
        nameElement.sendKeys(name);
    }

    public void typePassword(String password) {
        passwordElement.sendKeys(password);
    }

    public void clickLogin() {
        loginElement.click();
    }

    public void hideKeyboardIfVisible() {
        if (keyboard != null) {
            driver.hideKeyboard();
        }
    }

    public void login (String name, String password) {
        hideKeyboardIfVisible();
        typeName(name);
        typePassword(password);
        clickLogin();
    }
}
```

The element inspector and locator can be used to find the profile page class on the same manner as for the login page [above](https://blog.testproject.io/2018/07/14/page-object-model-appium-java-android/#ElementLocator).

![](https://blog.testproject.io/wp-content/uploads/2018/07/Android-Spy-2-512x369.png)

**Profile Page Class**:

```java
package io.testproject.appium.pom.tests.pages;

import io.appium.java_client.android.AndroidDriver;
import io.appium.java_client.android.AndroidElement;
import io.appium.java_client.pagefactory.AndroidFindBy;
import io.appium.java_client.pagefactory.AppiumFieldDecorator;
import org.openqa.selenium.support.PageFactory;

public class ProfilePage {

    private AndroidDriver driver;

    public ProfilePage() {
    }

    public ProfilePage(AndroidDriver driver) {
        this.driver = driver;
        PageFactory.initElements(new AppiumFieldDecorator(driver), this);
    }

    @AndroidFindBy(className = "UIAKeyboard")
    private AndroidElement keyboard;

    @AndroidFindBy(id = "greetings")
    private AndroidElement greetingsElement;

    @AndroidFindBy(id = "logout")
    private AndroidElement logoutElement;

    @AndroidFindBy(id = "country")
    private AndroidElement countryElement;

    @AndroidFindBy(id = "address")
    private AndroidElement addressElement;

    @AndroidFindBy(id = "email")
    private AndroidElement emailElement;

    @AndroidFindBy(id = "phone")
    private AndroidElement phoneElement;

    @AndroidFindBy(id = "save")
    private AndroidElement saveElement;

    @AndroidFindBy(id = "saved")
    private AndroidElement savedElement;

    public boolean isDisplayed() {
        return greetingsElement.isDisplayed();
    }

    public void typeCountry(String country) {
        countryElement.sendKeys(country);
    }

    public void typeAddress(String address) {
        addressElement.sendKeys(address);
    }

    public void typeEmail(String email) {
        emailElement.sendKeys(email);
    }

    public void typePhone(String phone) {
        phoneElement.sendKeys(phone);
    }

    public void hideKeyboardIfVisible() {
        if (keyboard != null) {
            driver.hideKeyboard();
        }
    }

    public void save() {
        saveElement.click();
    }

    public void updateProfile(String country, String address, String email, String phone) {
        hideKeyboardIfVisible();
        typeCountry(country);
        typeAddress(address);
        typeEmail(email);
        typePhone(phone);
        save();
    }

    public boolean isSaved() {
        return savedElement.isDisplayed();
    }

}
```

### **Create an Appium Page Object Test**

This test is identical to the one [above](https://blog.testproject.io/2018/07/14/page-object-model-appium-java-android/#AppiumTest) with the only difference that all the UI actions are now encapsulated into the pages classes.

Instead of searching and manipulating elements directly, this is being done using convenience methods (e.g.isDisplayed)that are implemented by every page.

```java
package io.testproject.appium.pom.tests;

import io.appium.java_client.android.AndroidDriver;
import io.appium.java_client.remote.AndroidMobileCapabilityType;
import io.appium.java_client.remote.MobileCapabilityType;
import io.testproject.appium.pom.tests.pages.LoginPage;
import io.testproject.appium.pom.tests.pages.ProfilePage;
import org.openqa.selenium.Platform;
import org.openqa.selenium.remote.DesiredCapabilities;

import java.net.URL;

public class PositiveLoginTest {

 private final static String APP_PACKAGE_NAME = "io.testproject.demo";
 private final static String APP_ACTIVITY_NAME = ".MainActivity";
 private final static String PASSWORD = "12345";

 public static void main(String[] args) throws Exception {

 // Prepare Appium session
 DesiredCapabilities capabilities = DesiredCapabilities.android();
 capabilities.setCapability(MobileCapabilityType.PLATFORM_NAME, Platform.ANDROID);
 capabilities.setCapability(MobileCapabilityType.UDID, "YOUR_DEVICE_UDID");
 capabilities.setCapability(MobileCapabilityType.NO_RESET, false);
 capabilities.setCapability(AndroidMobileCapabilityType.APP_PACKAGE, APP_PACKAGE_NAME);
 capabilities.setCapability(AndroidMobileCapabilityType.APP_ACTIVITY, APP_ACTIVITY_NAME);

 // Initialize driver
 AndroidDriver driver = new AndroidDriver(new URL("http://0.0.0.0:4723/wd/hub"), capabilities);

 driver.resetApp();

 LoginPage loginPage = new LoginPage(driver);
 if (!loginPage.isDisplayed()) {
 return;
 }

 loginPage.login("John Smith", PASSWORD);
 ProfilePage profilePage = new ProfilePage(driver);
 if (!profilePage.isDisplayed()) {
 return;
 }

 System.out.println("Test completed successfully");

 // Close session
 driver.quit();
 }
}
```

### **Example of Implementing Page Object Model with TestProject Framework**

This test can be enhanced even further by utilizing TestProject, so let's look at how to do that. The test logic stays identical to the previous examples, but, you will notice a few enhancements:

* The pages classes remain the same.
* Test class is annotated with @_Test_ annotation providing the test with a friendlier name.
* Calls to _report.step_ allow reporting of test milestones and provided better progress granulation when reviewing them in the results and reporting dashboard.
* The call to _report.result_ allows for providing a final statement for the test execution before it passes or fails.

```java
import io.testproject.java.annotations.v2.Parameter;
import io.testproject.java.annotations.v2.Test;
import io.testproject.java.enums.TakeScreenshotConditionType;
import io.testproject.java.sdk.v2.drivers.AndroidDriver;
import io.testproject.java.sdk.v2.enums.ExecutionResult;
import io.testproject.java.sdk.v2.exceptions.FailureException;
import io.testproject.java.sdk.v2.reporters.TestReporter;
import io.testproject.java.sdk.v2.tests.AndroidTest;
import io.testproject.java.sdk.v2.tests.helpers.AndroidTestHelper;

@Test(name = "Demo Test with Defaults")
public class DemoTestWithDefaults implements AndroidTest {

    @Parameter
    public String name = "John Smith";

    @Parameter
    public String password = "12345";

    @Parameter
    public String country = "Canada";

    @Parameter
    public String address = "8 Ness Ave";

    @Parameter
    public String email = "someone@somewhere.com";

    @Parameter
    public String phone = "+1 555 555";

    public ExecutionResult execute(AndroidTestHelper helper) throws FailureException {
        AndroidDriver driver = helper.getDriver();
        TestReporter report = helper.getReporter();

        driver.resetApp();

        LoginPage loginPage = new LoginPage(driver);
        report.step("Launched TestProject Demo app", loginPage.isDisplayed());

        loginPage.login(name, password);
        ProfilePage profilePage = new ProfilePage(driver);
        report.step(String.format("Logged in with %s:%s", name, password), profilePage.isDisplayed(), TakeScreenshotConditionType.Always);

        profilePage.updateProfile(country, address, email, phone);
        report.step(String.format("Profile information saved"), profilePage.isSaved(), TakeScreenshotConditionType.Always);

        report.result("Test completed successfully");
        return ExecutionResult.PASSED;
    }
}
```

To run the test locally, create a Runner as can be seen in the following example:

```java
import io.testproject.java.sdk.v2.Runner;

import java.io.IOException;

public class RunTests {
    private static Runner runner;

    public static void init() throws InstantiationException {
        runner = Runner.createAndroid("TP_DEV_TOKEN", "DEVICE_UDID", "io.testproject.demo", "io.testproject.demo.MainActivity");

    }

    public static void tearDown() throws IOException {
        runner.close();
    }

    public static void main(String[] args) throws Exception {
        init();
        runner.run(new DemoTestWithDefaults());
        tearDown();
    }
}
```



You can find more documentation for TestProject SDK here: [https://github.com/testproject-io/java-sdk-examples.](https://github.com/testproject-io/java-sdk-examples)
