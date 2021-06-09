# Running a Test Step Conditionally

Usually when you create a test step you want it to run every time you run the test, but sometimes, you only want a test step to run if certain conditions are met. TestProject allows you to do this with the [**Conditions** ](steps-widget.md#conditions)option in the advanced options section of a test step.

## How to Setup a Condition

Conditions are specified based on parameters. When you add a condition to a test step, you are prompted to select a parameter to use for that condition. Let's look at an example of how that might work

### Creating a test

Before looking at a condition, let's create a test so that you can see how it would work in the context of a 'typical' test script.

1. Setup a test using the TestProject example site \([https://example.testproject.io/](https://example.testproject.io/)\) and open the test in the Smart Recorder
2. Click on the Full Name text box and Type in a name
3. Click on the Password text box and type in `12345` as the password
4. Click on the login button
5. On the resulting page, fill out the fields in the form

### Creating a Condition

It's finally time to try out the condition option! Click on the Add step manually option and search for `random boolean` in the search field. Click on the result. If you do not already have the addon installed, TestProject will automatically install it for you.

In the output section click on the **Select parameter** field and use the blue plus button to create a new parameter. Name this parameter `randomBool` and change the type to be Output. Leave the value field blank

![Create an Output Parameter](../../.gitbook/assets/image%20%28179%29.png)

Save the parameter and then select it from the list and save the test step. This will automatically run the step and if you hover over the little green beside the test step, it will fly out and show you what value has been generated.

![View Generated Value](../../.gitbook/assets/image%20%28215%29.png)

Now, let's add a step that uses this value to conditionally run. Once again add a manually test step. Set the action to `click` and choose the `logout` element to act on. Expand the advanced options and under the conditions section choose to add a condition. Click the **Select parameter** dropdown and choose the `randomBool` parameter. Choose **Equals** from the operator dropdown and type `true` into the value field.

![Create a condition](../../.gitbook/assets/image%20%28209%29.png)

Save the test step and run it.

This is obviously a trivial example, but you may think of other ways when you would use this kind of functionality. In addition to examples like this where you can inject some randomness into your tests, you could have cleanup steps that you run if a certain condition is detected, or you could have a test that you use on a couple of very similar pages, but with a minor difference or two between each page that you account for with a condition.

This powerful option is just one more way that TestProject makes it easy for you to do exactly what you need to when creating tests.

