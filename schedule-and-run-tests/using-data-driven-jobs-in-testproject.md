# Using Data Driven Jobs in TestProject

Data driven testing is a powerful test automation concept that helps you leverage existing tests to quickly give you a lot of coverage for a particular variable. TestProject supports this approach and makes it easy to turn any test in the system into a data driven test. Data driven tests are tests that run multiple times, but with different values for some of the variables in the test. For example if you wanted to test that the username field on a login page could handle several different types of inputs you could create a separate test for each input, or you could use a data driven tests to drive the same login test multiple times, but just using a different username input each time. 

This tutorial will walk you through a specific example of creating a data driven test in TestProject so that you can see how to get started with using this powerful concept. 

## Parameterize Inputs

This tutorial will work off of a simple login test using the TestProject [sample site](https://example.testproject.io/web/). You can follow along with a tutorial that shows you how to create that test in the documentation section on [creating a web test](../using-the-smart-test-recorder/web-testing/creating-a-web-test-using-the-testproject-recorder.md).

Once you have a test setup, the first thing you will need to do is to parameterize the variable that you want to use to drive the test. In this example that will be in the input to the full name field of the login form. To do that open the test in the test editor by clicking on it in the project view. You can then open the parameters panel for that test from the more menu.

![Access Test Parameters](../.gitbook/assets/image%20%2825%29.png)

You can then add a new parameter with the plus button at the bottom of the panel.

![Add New Parameter](../.gitbook/assets/image%20%2813%29.png)

Fill in the name, description and value for the parameter and click on the add button to add it to your test.

![Add a Parameter](../.gitbook/assets/image%20%2810%29.png)

This parameter is now ready to be used in the test. Navigate to the test step where you want to use it and click on that step in the step editor. Find the Input parameters section on the editing panel and click on the plus beside the input parameter you are interested in.

![Add an input parameter](../.gitbook/assets/image%20%283%29.png)

Clear any text already entered and then choose the parameter you created from the list of parameters.

![Pick Parameter](../.gitbook/assets/image%20%284%29.png)

This will add the parameter as a variable in the input field and you can click on the check mark at the bottom of the panel to apply the change. 

![Apply Changes](../.gitbook/assets/image%20%2817%29.png)

Click on the Save button on the test step panel and you will now have your input field parameterized.

## Generating a Data Source

In order to run a data driven test, you will need to create the data that you want to use and add it to the system. An easy way to get started with that is to go to the test you want to generate data for and use the more menu on it to download a Data Source Template.

![Data Source Template](../.gitbook/assets/image%20%2837%29.png)

This will download a .csv file to your computer with headers for each of the parameters you have defined in your test. You can open the file in Excel or any other spreadsheet editing program and add in rows for each input you want to add.

![Create Data](../.gitbook/assets/image%20%2814%29.png)

Once you have added the data that you want you can save the file as a .csv file again and upload it back into the TestProject app. To do that, go to the Data Sources menu option and choose to Add a data file.

![Add a data file](../.gitbook/assets/image%20%2823%29.png)

Choose the .csv file you created and give it a name on click on Create. This will add the file to the system as an input source that you can use

## Running Tests with a Data Source

Now that there is a data source in your project you can use it to drive your test. Click on Run icon for the test and choose the agent and platform that you will run the test on.

![Run a Test](../.gitbook/assets/image%20%2818%29.png)

On the next page, you will be prompted for fill in the parameters for that test. To run a data driven test, enable the Override default input parameters option.

![Override default input parameters](../.gitbook/assets/image%20%286%29.png)

You can then select the data source you previously added and click on run.  The test will run once for each row that you have added in the .csv file using the input for that row.

