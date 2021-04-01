---
description: Python OpenSDK
---

# Python

## Getting started

To get started, you need to complete the following prerequisites checklist:

* Login to your account at [https://app.testproject.io/](https://app.testproject.io/) or [register a new one](https://app.testproject.io/signup/).
* [Download](https://app.testproject.io/#/download) and install an Agent for your operating system or pull a container from [Docker Hub](https://hub.docker.com/r/testproject/agent).
* Run the Agent and [register it](https://docs.testproject.io/getting-started/installation-and-setup#register-the-agent) with your Account.
* Get a development token from the [Integrations / SDK](https://app.testproject.io/#/integrations/sdk) page.

### Installation

The TestProject Python SDK is [available on PyPI](https://pypi.org/project/testproject-python-sdk/). All you need to do is add it as a Python module using:

```text
pip3 install testproject-python-sdk
```

and you're good to go.

## Test Development

Using a TestProject driver is identical to using a Selenium driver. Once you have added the SDK as a dependency to your project, changing the import statement is enough in most cases.

You can create a TestProject-powered version of a test using Chrome by using the TestProject Chrome driver:

```text
# from selenium import webdriver  <-- replace this import
from src.testproject.sdk.drivers import webdriver

def test_create_a_chrome_driver_instance():
    driver = webdriver.Chrome()
    # Your test code goes here
    driver.quit()
```

Here's an example of a complete test that is using the Chrome driver from the TestProject SDK:

```text
from src.testproject.sdk.drivers import webdriver

def simple_test():
    driver = webdriver.Chrome()

    driver.get("https://example.testproject.io/web/")

    driver.find_element_by_css_selector("#name").send_keys("John Smith")
    driver.find_element_by_css_selector("#password").send_keys("12345")
    driver.find_element_by_css_selector("#login").click()

    passed = driver.find_element_by_css_selector("#logout").is_displayed()

    print("Test passed") if passed else print("Test failed")

    driver.quit()

if __name__ == "__main__":
    simple_test()
```

## Drivers

The TestProject SDK overrides standard Selenium/Appium drivers with extended functionality.

The examples shown in this document are based on Chrome. The SDK works in the same way for all other supported browsers:

* Firefox
* Safari
* Edge
* Internet Explorer
* Android apps \(using Appium\)
* iOS apps \(using Appium\)

### Development token

The SDK uses a development token for communication with the Agent and the TestProject platform. To configure your development token for use with the SDK, you have to specify it in an environment variable `TP_DEV_TOKEN`.

Alternatively, you can pass in your developer token as an argument to the driver constructor:

```text
def test_create_a_chrome_driver_instance():
    driver = webdriver.Chrome(token='YOUR_TOKEN_GOES_HERE')
    # Your test code goes here
    driver.quit()
```

### TestProject Agent

By default, drivers communicate with the local Agent listening on [http://localhost:8585](http://localhost:8585/). This value can be overridden by setting the `TP_AGENT_URL` environment variable to the correct Agent address.

### Remote \(Cloud\) Driver

By default, TestProject Agent communicates with the local Selenium or Appium server. In order to initialize a remote driver for cloud providers such as SauceLabs or BrowserStack, a custom capability `cloud:URL` should be set, for example:

```text
def driver():
    chrome_options = ChromeOptions()
    chrome_options.set_capability("cloud:URL", "https://{USERNAME}:{PASSWORD}@ondemand.us-west-1.saucelabs.com:443/wd/hub")
    driver = webdriver.Chrome(chrome_options=chrome_options, projectname="Examples")
    yield driver
    driver.quit()
```

## Reports

By default, the TestProject SDK reports all executed driver commands and their results to the TestProject Cloud. This allows us to create and display detailed HTML reports and statistics in your project dashboards.

Reports can be completely disabled using this driver constructor:

```text
def test_disable_reporting():
    driver = webdriver.Chrome(disable_reports=True)
    # no reports will be created for this test
    driver.quit()
```

### Implicit project and job names

The SDK will attempt to infer Project and Job names when you use pytest or unittest. For example:

* when using **pytest**, tests in the `my_tests.py` module in the `e2e_tests/chrome` package will be reported with a project name `e2e_tests.chrome` and job name `my_tests`.
* when using **unittest**, tests in the `my_tests.py` module in the `e2e_tests/chrome` package will be reported with a project name `chrome` and job name `my_tests`.

Examples using inferred project and job names:

* [pytest](https://github.com/testproject-io/python-sdk/blob/master/tests/examples/frameworks/pytest/implicit_report_test.py)
* [unittest](https://github.com/testproject-io/python-sdk/blob/master/tests/examples/frameworks/unittest/implicit_report_test.py)

### Explicit project and job names

Project and Job names can be also specified explicitly using this constructor:

```text
def test_specify_project_and_job_names_in_driver_constructor():
    driver = webdriver.Chrome(projectname='My custom project', jobname='My custom job')
    # Your test code goes here
    driver.quit()
```

or using the `@report` decorator:

```text
from src.testproject.decorator import report

@report(project='My project', job='My job')
def test_specify_project_and_job_name_in_decorator():
    driver = webdriver.Chrome()
    # Your test code goes here
    driver.quit()
```

Examples using explicitly specified project and job names:

* [pytest](https://github.com/testproject-io/python-sdk/blob/master/tests/examples/frameworks/pytest/explicit_report_test.py)
* [unittest](https://github.com/testproject-io/python-sdk/blob/master/tests/examples/frameworks/unittest/explicit_report_test.py)

## Test reports

### Cloud and Local Report

By default, the execution report is uploaded to the cloud, and a local report is created, as an HTML file in a temporary folder.

At the end of execution, the report is uploaded to the cloud, and SDK outputs to the console/terminal the path for a local report file:

Execution Report: {temporary\_folder}/report.html

This behavior can be controlled, by requesting only a LOCAL or only a CLOUD report.

> When the Agent is offline, and only a \_cloud\_ report is requested, execution will fail with appropriate message.

Via a driver constructor:

```text
driver = webdriver.Chrome(report_type=ReportType.LOCAL)
```

### Automatic test reporting

Tests are reported automatically when a test ends or when the `quit()` command is called on the driver. This behavior can be overridden or disabled \(see the [Disabling Reports]() section below\).

In order to determine whether a test has ended, the call stack is inspected, searching for the current test method. When the test name is different from the latest known test name, it is concluded that the execution of the previous test has ended. This is supported for both pytest and unittest.

To override the inferring of the test name and specify a custom test name instead, you can use the `@report` decorator:

```text
from src.testproject.decorator import report

@report(test='My test name')
def test_specify_test_name_in_decorator():
    driver = webdriver.Chrome()
    # Your test code goes here
    driver.quit()
```

Here is a complete example using [automatic reporting](https://github.com/testproject-io/python-sdk/blob/master/tests/examples/reports/automatic_reporting_test.py).

#### Manual test reporting

To report tests manually, you can use `driver.report().test()`:

```text
def test_report_test_manually():
    driver = webdriver.Chrome()
    # Your test code goes here
    driver.report().test(name='My test name', passed=True)
    driver.quit()
```

#### Reporting steps

Steps are reported automatically for every driver commands that is executed. If this feature is disabled, or you would like to add steps manually, you can use `driver.report().step()`:

```text
def test_report_step_manually():
    driver = webdriver.Chrome()
    # Your test code goes here
    driver.report().step(description='My step description', message='An additional message', passed=False, screenshot=True)
    driver.quit()
```

Here is a complete example using [manual test reporting of tests and steps](https://github.com/testproject-io/python-sdk/blob/master/tests/examples/reports/manual_reporting_test.py).

### Disabling reports

If reports were not disabled when the driver was created, they can be disabled or enabled later. However, if reporting was explicitly disabled when the driver was created, they **cannot** be enabled later.

#### Disable all reports

The following will temporarily disable all reporting:

```text
def test_temporarily_disable_all_reporting_then_reenable_it_later():
    driver = webdriver.Chrome()
    driver.report().disable_reports(True)
    driver.find_element_by_id('your_element_id').click()  # This statement will not be reported
    driver.report().disable_reports(False)
    driver.quit()
```

#### Disable automatic test reports

The following will disable automatic reporting of tests. All steps will end up in a single test report, unless tests are reported manually using `driver.report().test()`:

```text
def test_disable_automatic_test_reporting():
    driver = webdriver.Chrome()
    driver.report().disable_auto_test_reports(True)
    # Tests will not be reported automatically from here on
    driver.quit()
```

#### Disable driver command reports

The following will disable driver command reporting, which results in the reporting of tests that will have no steps, unless reported manually using `driver.report().step()`:

```text
def test_disable_automatic_reporting():
    driver = webdriver.Chrome()
    driver.report().disable_command_reports(True)
    # From here on, driver commands will not be reported automatically
    driver.quit()
```

#### Disable driver command redaction

When driver commands are being reported, the SDK will, by default, redact the values typed into sensitive elements by replacing the actual text with three asterisks \(`***`\) in the report. Elements are considered sensitive if they:

* have an attribute `type` with value `password` \(all browsers and platforms\)
* are of type `XCUIElementTypeSecureTextField` \(iOS / XCUITest only\)

This redaction of sensitive commands can be disabled, if desired:

```text
def test_disable_driver_command_report_redaction():
    driver = webdriver.Chrome()
    driver.report().disable_redaction(True)
    # From here on, driver commands will not be redacted
    driver.quit()
```

If no test name is specified using the decorator, the test method name will be used as the test name in the report.

### The importance of using `quit()`

Even more so than with regular Selenium- or Appium-based tests, it is important to make sure that you call the `quit()` method of your TestProject driver object at the end of every test that uses the TestProject SDK.

Upon calling `quit()`, the SDK will send all remaining report items to the Agent, ensuring that your report on the TestProject platform is complete.

**Tip for pytest users**: use a [pytest fixture](https://docs.pytest.org/en/stable/fixture.html#fixtures-as-function-arguments) to ensure that `quit()` is called at the end of the test, even when an error occurred during test execution:

```text
import pytest

@pytest.fixture
def driver():
    driver = webdriver.Chrome()
    yield driver
    driver.quit()

def test_using_pytest_fixture(driver):
    driver.get("https://example.testproject.io/web")
```

**Tip for unittest users**: use the `setUp()` and `tearDown()` [methods](https://docs.python.org/3/library/unittest.html#organizing-tests) for driver creation and destroying:

```text
import unittest

class ChromeTest(unittest.TestCase):

    def setUp(self):
        self.driver = webdriver.Chrome()

    def test_using_unittest_setup_and_teardown(self):
        driver.get("https://example.testproject.io/web")

    def tearDown(self):
        self.driver.quit()
```

### Logging

The TestProject Python SDK uses the `logging` framework built into Python. The default logging level is `INFO` and the default logging format is `%(asctime)s %(levelname)s %(message)s`, which results in log entries formatted like this:

`13:37:45 INFO Using http://localhost:8585 as the Agent URL`

If you wish, you can override the default log configuration:

* For **pytest** users, it is recommended to provide alternative values [in your pytest.ini](https://docs.pytest.org/en/latest/reference.html#ini-options-ref)
* Users of **unittest** can override the configuration by setting the `TP_LOG_LEVEL` and / or `TP_LOG_FORMAT` environment variables, respectively, to the desired values

See [this page](https://docs.python.org/3/library/logging.html#logging-levels) for a list of accepted logging levels and [look here](https://docs.python.org/3/howto/logging.html#changing-the-format-of-displayed-messages) for more information on how to define a custom logging format.

### Examples

Here is a list of all examples for the different drivers that are supported by this SDK:

_Web_

* [Chrome test](https://github.com/testproject-io/python-sdk/blob/master/tests/examples/drivers/web/chrome_driver_test.py)
* [Firefox test](https://github.com/testproject-io/python-sdk/blob/master/tests/examples/drivers/web/firefox_driver_test.py)
* [Safari test](https://github.com/testproject-io/python-sdk/blob/master/tests/examples/drivers/web/safari_driver_test.py)
* [Edge test](https://github.com/testproject-io/python-sdk/blob/master/tests/examples/drivers/web/edge_driver_test.py)
* [Internet Explorer test](https://github.com/testproject-io/python-sdk/blob/master/tests/examples/drivers/web/ie_driver_test.py)

_Android_

* [Android native test](https://github.com/testproject-io/python-sdk/blob/master/tests/examples/drivers/android/android_driver_test.py)
* [Android native app](https://github.com/testproject-io/android-demo-app)
* [Web test on mobile Chrome](https://github.com/testproject-io/python-sdk/blob/master/tests/examples/drivers/android/android_driver_chrome_test.py)

_iOS_

* [iOS native test](https://github.com/testproject-io/python-sdk/blob/master/tests/examples/drivers/ios/ios_driver_test.py)
* [iOS native app](https://github.com/testproject-io/ios-demo-app)
* [Web test on mobile Safari](https://github.com/testproject-io/python-sdk/blob/master/tests/examples/drivers/ios/ios_driver_safari_test.py)

### License

The TestProject Python SDK is licensed under the LICENSE file in the root directory of the project source tree.

