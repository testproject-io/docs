---
description: Learn about the different types and option when using Parameters
---

# Using Parameters Effectively

Parameters are a powerful way to make your tests more maintainable. They also make it easy to share inputs and outputs between test steps or even between tests in a project.

## Create Parameters

You can see and manage all the parameters for a test by clicking on the test in the project view to open it in the recorder and then choosing Parameters.

![Opening parameters tab](<../.gitbook/assets/image (456).png>)

This will open the parameters panel for you where you can view, edit, add or remove parameters for the test. Parameters can be created that are **only** for the particular test you are working on (Test Parameters), or they can be created at the project level so that you can use the same parameter in **multiple** tests (Project Parameters). You can add a new parameter with the plus button at the bottom of the panel.

![Create new Parameter](<../.gitbook/assets/image (454).png>)

Fill in the name, description, value, secret, and type for the parameter and click on the Save button to add it to your test.

![Creating Parameter](<../.gitbook/assets/image (458).png>)

## Parameters types

### Input Parameter

Should be used for any parameter that we want to change during test setup for example [data-driven test](https://docs.testproject.io/schedule-and-run-tests/using-data-driven-jobs-in-testproject), passing data into a sub-test, and changing the parameters before test execution.&#x20;

### Output Parameters

Should be used to return information from a [sub-test](using-page-object-model-and-page-factory-with-testproject.md#page-object-in-recorded-tests) to the main test.

### Private Parameters

Use private when the parameter value should not be defined during the test setup. For example, When the get text action is used and a parameter captures the value for comparison during the test, this parameter inherits its value from an element inside the test, and therefore should be set to private. (as there is no reason to override the parameter value with a data source).&#x20;

## Secret Parameters

The Secret parameters option allows us to define a special parameter that can be used to store sensitive information safely and hide it from the test report.

{% hint style="success" %}
Useful for sensitive information such as passwords, API tokens, or other login credentials.
{% endhint %}

Unlike regular parameters, secret parameters values are stored in an **encrypted state** and can not be viewed by anyone. After setting the value of a secret parameter, it is only possible to replace it with a new value. The Secret parameter values will be **hidden from the reports** and in no case are stored as plain text.

## Input and Output Fields

To use parameters in the test we need to assign them in specific fields.

{% hint style="info" %}
An input field can be populated by an output type parameter, and an input type parameter can be used on an output field. Their differences are explained [above](using-parameters-effectively.md#parameters-types).
{% endhint %}

### Input Fields&#x20;

Some actions allow you to input data into the step to use while executing, for example, type text action allows you to type a specific text or any string that you wish to type, or you can use a parameter to **dynamically** pass the data during the test execution.

### Output fields

Some actions also return information after they are executed. for example, the get text action allows you to specify an element you want to retrieve the text from. Then a parameter can be used on the output field to **capture** the data returned from the step, in this case, the text.

## Sharing Parameters

The whole point of parameterizing something is so that you can use the same value in multiple places. This makes it much easier to maintain since you only need to update the value in one place if you are making changes. It also helps to ensure that you have consistency in your tests.&#x20;

However, there are some things to be careful of when it comes to sharing parameters. In general sharing parameters within a test is pretty safe, but when using a parameter at the project level it is important to think about the fact that you might want to **run tests at different times and in different orders or even simultaneously**.

You want to make sure that you do not create dependencies between tests, where one test can only run properly if another test has already been run. This is especially important with output parameters. In general, you do not want to use an output parameter from one test as an input parameter in another test.

## Using Parameters

After we have created the parameter it is now ready to be used in the test. parameters can be used in multiple test steps and can also be used for [data-driven testing](../schedule-and-run-tests/using-data-driven-jobs-in-testproject.md).&#x20;

You can access the parameters directly from a test step (for actions that with input/output fields), by clicking on the blue "Parameter" label on top of the input field or on the "Select parameter" option on the output fields in the steps.

![Using a parameter in both input and output fields](<../.gitbook/assets/image (468) (1).png>)

Parameters can also be used in combination with static text for example validating the welcome message on our example login page:&#x20;

![Using a parameter with text](<../.gitbook/assets/image (455).png>)



