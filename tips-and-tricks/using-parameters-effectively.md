# Using Parameters Effectively

Parameters are a powerful way to make your tests more maintainable. They also make it easy to share inputs and outputs between test steps or even between tests in a project.

## Input Parameters

You can see and manage all the parameters for a test by clicking on the test in the project view to open it in the recorder and then choosing Parameters from the more menu

![Access Test Parameters](../.gitbook/assets/image%20%2827%29.png)

This will open the parameters panel for you where you can view, edit, add or remove parameters for the test. Parameters can be created that are only for the particular test you are working on, or they can be created at the project level so that you can use the same parameter in multiple tests. You can add a new parameter with the plus button at the bottom of the panel.

![Add New Parameter](../.gitbook/assets/image%20%2815%29.png)

Fill in the name, description and value for the parameter and click on the add button to add it to your test.

![Add a Parameter](../.gitbook/assets/image%20%2812%29.png)

This parameter is now ready to be used in the test. You can also access the parameters directly from a test step \(for actions that can have parameters\), by click on the + button beside the parameter input box.

![Access Test Parameters](../.gitbook/assets/image%20%2824%29.png)

## Output Parameters

Some actions also allow you to specify output parameters. Output parameters are a place to store the result of the action. When creating a new output parameter, leave the value empty as it will be filled in by the test. You can then use that parameter elsewhere in the test. 

## Sharing Parameters

The whole point of parameterizing something is so that you can use the same value in multiple places. This makes it much easier to maintain since you only need to update the value in one place if you are making changes. It also helps to ensure that you have consistency in your tests. 

However, there are some things to be careful of when it come to sharing parameters. In general sharing parameters within a test is pretty safe, but when using a parameter at the project level it is important to think about the fact that you might want to run tests at different times and in different orders. You want to make sure that you do not create dependencies between tests, where one test can only run properly if another test has already been run. This is especially important with output parameters. In general you do not want to use an output parameter from one test as an input parameter in another test.

## Using Parameters

Parameters can be used in multiple test steps and can also be used for [data driven testing](../schedule-and-run-tests/using-data-driven-jobs-in-testproject.md). To use them, select the + button beside the parameter input box you are interested in and select or create the parameter you want to use. If you don't want the current text, clear it and then choose the parameter you created from the list of parameters.

![Pick Parameter](../.gitbook/assets/image%20%285%29.png)

This will add the parameter as a variable in the input field and you can click on the check mark at the bottom of the panel to apply the change. 

![Apply Changes](../.gitbook/assets/image%20%2819%29.png)

Click on the Save button on the test step panel and you will now have your input field parameterized. You can use multiple parameters in one input field by clicking on them in the list. You can also include non-parameterized values with parameters in the same field if you want. For example, you could parameterize both the first name and last name values and use a manually entered string like Mr. all in the same input field

![Multiple Parameters](../.gitbook/assets/image%20%2832%29.png)







