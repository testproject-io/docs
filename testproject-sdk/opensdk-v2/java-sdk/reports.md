# Reports

The Test ProjectSDK tightly integrates with the TestProject application. Test that are run with the SDK, can send data to TestProject application so that you can use the powerful reporting functionaliy in there to view and share information about test runs. 

## Naming Projects

When running tests with the SDK, TestProject will automaticaly create a project for you so that it can use if for reporting.  This project needs to have a name. You can explicitly set that name wiht the constructor if you want.

### Explicit Names

Project and Job names can be specified explicitly using this constructor:

```text
public ChromeDriver(final ChromeOptions options, final String projectName, final String jobName)
```

For example the following code would create a project called **My First Project**  and the job that ran tests using this would be called **My First Job** :

```text
ChromeDriver driver = new ChromeDriver(new ChromeOptions(), "My First Project", "My First Job");
```

Alternatively, you could do this with the  `DriverBuilder`using code like this:

```text
ChromeDriver driver = new DriverBuilder<ChromeDriver>(new ChromeOptions())
  .withProjectName("My First Project")
  .withJobName("My First Job")
  .build(ChromeDriver.class);
```

You can see some example of examples of tests using explicit Project & Job names configuration in the following files:

* [JUnit 5 example](https://github.com/testproject-io/java-sdk/blob/master/src/test/java/io/testproject/sdk/tests/examples/frameworks/junit5/ExplicitReportTest.java)
* [TestNG example](https://github.com/testproject-io/java-sdk/blob/master/src/test/java/io/testproject/sdk/tests/examples/frameworks/testng/ExplicitReportTest.java)

### Implicit Names

If you do not explicitly specify project and job names, the SDK will attempt to infer them from JUnit / TestNG annotations.

It will use the following logic when naming projects and jobs in the TestProject App:

* _Package_ name of the class containing the method is used for **Project** name.
* JUnit 4 / 5
  * _Class_ name or the _@DisplayName_ annotation \(JUnit 5 only\) on the class is used for the **Job** name
  * _Method_ name or the _@DisplayName_ annotation \(JUnit 5 only\) on the method is used for the **Test** name\(s\)
* TestNG
  * _Class_ name or _description_ from _@BeforeSuite_ / _@BeforeClass_ annotations if found, are used for the **Job** name
  * _Method_ name or the _@Test_ annotation \(and it's _testName_ / _description_ fields\) on the method is used for the **Test** name\(s\)

You can see some example of examples of tests using implicit Project & Job names inferred from annotations at these links:

* [JUnit 5 example](https://github.com/testproject-io/java-sdk/blob/master/src/test/java/io/testproject/sdk/tests/examples/frameworks/junit5/InferredReportTest.java)
* [TestNG example](https://github.com/testproject-io/java-sdk/blob/master/src/test/java/io/testproject/sdk/tests/examples/frameworks/testng/InferredReportTest.java)

## Automatic Tests Reporting

Tests are reported automatically when a test **ends** or when driver _quits_.  
 This behavior can be overridden or disabled.

In order to determine that a test ends, the call stack is traversed searching for an annotated methods. When an annotated method execution starts and a previously detected one ends, it is assumed that a test has completed. 

Any unit testing framework annotations is considered, creating a _separate_ test in the report for every annotated method. For example, the following JUnit based code, will generate the following _six_ tests in the report:

```text
@BeforeEach
void beforeTestExample(TestInfo testInfo) {
    driver.report().step("Preparing Test: " + testInfo.getDisplayName());
}

@Test
@DisplayName(value = "Google")
void testGoogle() {
    driver.navigate().to("https://www.google.com/");
}

@Test
@DisplayName(value = "Yahoo!")
void testYahoo() {
    driver.navigate().to("https://yahoo.com/");
}

@AfterEach
void afterTestExample(TestInfo testInfo) {
    driver.report().step("Finishing Test: " + testInfo.getDisplayName());
}
```

Report:

```text
Report
├── beforeTestExample
│   ├── Preparing Test: Yahoo!
├── Yahoo! Test
│   ├── Navigate To https://yahoo.com/
├── afterTestExample
│   ├── Finishing Test: Yahoo!
├── beforeTestExample
│   ├── Preparing Test: Google
├── Google Test
│   ├── Navigate To https://google.com/
└── afterTestExample
    └── Finishing Test: Google
```

You can see a complete example with automatic test reporting [here](https://github.com/testproject-io/java-opensdk/blob/master/src/test/java/io/testproject/sdk/tests/examples/reports/AutomaticReporting.java).

### **Limitations**

JUnit5 dynamic test names cannot be inferred, and should be reported manually. These will be reported as _Dynamic Test_ when reported automatically.

## Manual Tests Reporting

To report tests manually, use `driver.report().tests()` method and it's overloads. For example:

```text
ChromeDriver driver = new ChromeDriver(new ChromeOptions());
driver.report().disableTestAutoReports(true);
driver.report().test("My First Test").submit();
```

> It's important to [disable automatic test reporting ](reports.md#disabling-reports)when using the manual option to avoid collision.

Note that `driver.report().test()` returns a `ClosableTestReport` object. An explicit call to `submit()` or closing the object is required for the report to be sent.

Using this closable object can be beneficial in the following case:

```text
ChromeDriver driver = new ChromeDriver(new ChromeOptions());
try (ClosableTestReport report = driver.report().test("Example Test with Exception")) {
  driver.findElement(By.id("NO_SUCH_ELEMENT")).click();
}
```

Assuming there is no element on the DOM with such an ID: `NO_SUCH_ELEMENT`, an exception will be thrown and test will fail, but before that, the closable object will get closed and so the test will still be reported.

You can see a complete example with manual test reporting [here](https://github.com/testproject-io/java-opensdk/blob/master/src/test/java/io/testproject/sdk/tests/examples/reports/ManualReporting.java).

### Steps

Test steps are reported automatically when driver commands are executed. If this feature is disabled, or in addition, manual reports can be performed, for example:

```text
ChromeDriver driver = new ChromeDriver(new ChromeOptions());
driver.report().step("User logged in successfully");
```

## Disabling Reports

If you don't want to see reports for your runs, you can disable them by setting the `disableReports` option in the constructor.

```text
public ChromeDriver(final ChromeOptions options, final boolean disableReport
```

{% hint style="info" %}
If reports were **not** disabled when the driver was created, they can be disabled or enabled later. However, if reporting was explicitly disabled when the driver was created, it can **not** be enabled later in the file.
{% endhint %}

### Disable all reports

The following code will disable all types of reports:

```text
ChromeDriver driver = new ChromeDriver(new ChromeOptions());
driver.report().disableReports(true);
```

### Disable tests automatic reports

If you only want to disable automatic reports, but still allow for manul reporting, you can use the the following code:

```text
ChromeDriver driver = new ChromeDriver(new ChromeOptions());
driver.report().disableTestAutoReports(true);
```

When you do this, all test steps will reside in a single test report, unless the tests are reported manually using `driver.report().tests()`:

### Disable driver commands reports

The following code will disable the reporting of driver _commands._

```text
ChromeDriver driver = new ChromeDriver(new ChromeOptions());
driver.report().disableCommandReports(true);
```

In the case, the report will have no steps, unless they are reported manually using `driver.report().step()`:

### Disable commands redaction

When reporting driver commands, the SDK performs a redaction of sensitive data \(values\) sent to secured elements. If the element is one of the following:

* Any element with `type` attribute set to `password`
* With XCUITest, on iOS an element type of `XCUIElementTypeSecureTextField`

Values sent to these elements will be converted to three asterisks - `***`. This is here for security purposes, but if you want to you can disabled it with the following code:

```text
ChromeDriver driver = new ChromeDriver(new ChromeOptions());
driver.report().disableRedaction(true);
```

