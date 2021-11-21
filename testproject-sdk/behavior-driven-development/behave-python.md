---
description: Perform Behavior Driven Development with the Python OpenSDK.
---

# Behave (Python)

The TestProject Python OpenSDK supports automatic reporting of Behave features, scenarios and steps using the **@behave\_reporter** annotation.

While utilizing the TestProject OpenSDK with Behave you will be able to collaborate with your team members in the cloud , share reports, screenshots and automation progress.

You can install Behave with the following command:

`pip install behave`

Using the annotation will disable the reporting of driver command and automatic reporting of tests.

Instead, it will report:

* A test for every scenario in a feature file
* All steps in a scenario as steps in the corresponding test
* Steps are automatically marked as passed or failed, including the cause of failure.

To enable Behave feature reporting, in your **environment.py** annotate the following methods:

* method used to initialize your driver (usually, **before\_all**, **before\_feature **or a **fixture**)
* **after\_step**
* **after\_scenario**

```
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

Screenshots by default are only taken on step failure, you can however override this behavior by passing the **screenshot** argument as **True **in your annotation.

```
@behave_reporter(screenshot=True)
after_step(context, step):
    pass
```

### Example

The following is an example of using TestProject with the Behave framework.

If you are using PyCharm as your IDE, it is recommended to install the Gherkin plugin for feature file syntax highlighting and execution.

The plugin can be found through the file > settings > Plugins section.

![Gherkin Plugin](<../../.gitbook/assets/image (281).png>)

After creating a features directory and adding a feature file, these are just files with the .feature extension.

For example:

```
Feature: TestProject with Behave Framework

  Scenario: Run a Simple BDD test with TestProject
     Given I navigate to the TestProject example page
     When I perform a login
     Then I should see a logout button
```

If you have the plugin installed, you can right click on the definitions in the feature file, and use the context actions to quickly create all the step definition templates for the feature.

![Context Actions](<../../.gitbook/assets/image (278).png>)

The following file will be created, and your feature file will know where to search for the step definitions when executed.

```
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

In the same features directory, create a file called** environment.py. **

Behave uses the environment file to define hooks that will be called before or after each step, scenario, feature or even entire test run.

Inside the environment file, create the **after\_step(context, step)** and **after\_scenario(context, scenario) **methods and annotate them with the **@behave\_reporter** annotation.

{% hint style="info" %}
**Please make sure to also annotate the method used to construct the TestProject driver. Usually the driver is constructed in the environment.py file under a before\_all(context), before\_feature(context, feature) hooks or before\_tag(context, ** **tag) hook using a fixture to guarantee the driver is initialized before the test run.**
{% endhint %}

If you do not want to perform any additional operations after each step or scenario, you can use **pass **in the method.

Example of an **environment.py** file:

```
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

By creating the driver in the **before\_all **hook and storing it in the Behave context, we can use the driver in all other methods using the context after the hook method call, meaning that we have direct access the the driver in all the following hooks, and even our step implementations.

The following will be our step implementations, performing a simple login scenario and validation on Chrome using the TestProject example page:

```
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

![Project Structure](<../../.gitbook/assets/image (276).png>)

PyCharm Professional allows you to run your Behave via a run configuration setting:

![Run Configuration 1](<../../.gitbook/assets/image (269).png>)

![Run configuration 2](<../../.gitbook/assets/image (272).png>)

Where the file path specified is the directory containing your feature files.

You can also run the features from the terminal by using the following command:

`behave path/to/features/directory`

The example code is available in the Python OpenSDK GitHub documentation [here](https://github.com/testproject-io/python-sdk/tree/master/tests/examples/frameworks/behave/features).
