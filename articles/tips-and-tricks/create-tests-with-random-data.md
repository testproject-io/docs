# Create Tests with Random Data

Data inputs in tests are important. Often automated tests will require data to be input. Sometimes data needs to be in a certain format, for example if testing a field that take in an email address or a phone number, but you may not want to just use the exact same data every time. By using the same data every time we test a certain kind of field we can be opening up the application to risk that it might not work with other inputs. One way to overcome this is by using random data. You could just generate totally random strings, but often you want data of a particular type. You may want an address, or a name or a date or various other types of random data that is formatted in a particular way.&#x20;

This is where some of the powerful random data generate addons in TestProject come in. Let's take a look at an example using some of these addon actions.&#x20;

## Getting Started

This example will use the [TestProject Example site](https://example.testproject.io/web/) and you can see how to set up a project and initialize a test with this in the [web testing](../../using-the-smart-test-recorder/web-testing/creating-a-web-test-using-the-testproject-recorder.md) section of the documentation. Load the application in the TestProject recorder and let's look at entering some random data into the form.

## Login Page

The first thing to test is the login page. Click on the Full Name field and a step will be added to the test. Now add a new step using the plus button.

Click on this most recently created test step and make some changes to it. Change the type of the test step from Element Action to Action.

![Change the type to Action](<../../.gitbook/assets/image (189) (1).png>)

Next click on the select action link and search for `random name` in the search box. In the search results notice that there is a Random name action. This action is available in the jRand addon. There is more information on how to install and use addons in the documentation [here](../../testproject-addons/using-addons-in-the-testproject-recorder.md). With the jRand addon installed click on that action to select it to add it to the test step. Under the Output parameters section of the test step, click on the Select Parameter link.

![Select Parameter](<../../.gitbook/assets/image (45).png>)

Use the plus icon on the bottom of the panel to add a new parameter

![Add New Parameter](<../../.gitbook/assets/image (142).png>)

Name the parameter, but leave the value field blank (it will be filled in by the addon) and click Add to add that parameter to the test.

Now use the More menu on the test step created when the Full Name box was clicked and select the Duplicate option to create a duplicate of that test step

![Duplicate Test Step](<../../.gitbook/assets/image (59).png>)

Take this duplicate test step and drag it to the end of the test and click on it. The action for this test step is set to Click. Click on that action and search for type text. Select that action and then in the input parameters section choose the plus beside the input box to select a parameter for this input.

![Use a Parameter](<../../.gitbook/assets/image (55) (1).png>)

Choose the parameter you created above and then click on the check mark at the bottom of the panel to use that parameter in this test step

![Choose Parameter](<../../.gitbook/assets/image (191).png>)

Save the Test Step and then use the Run until here option from the more menu to run the test and notice that a random name has been input into the Full Name textbox.

![Random Full name](<../../.gitbook/assets/image (81) (2).png>)

Click on the password box and type `12345`to enter the password and then click login. This will add those actions as steps to the test.

## Filling in the Form

On the form page there are a number of different input types. The country is just a select dropdown. Click on that and select a country from the list to add test steps for that. Similary for the address field, type in an address.&#x20;

Click on the email field and then duplicate the step that gets added to the test. On the duplicated test step, change the Type from Element Action to Action and then search for `random email` and choose the random email address option.&#x20;

Follow a similar process for the Phone number field.

## Conclusion

TestProject addons provide a lot of power and flexibility when it comes to generating and using random data. With a quick and simple install of a couple of addons, you are able to effectively integrate this testing strategy into you test with a single click.&#x20;

