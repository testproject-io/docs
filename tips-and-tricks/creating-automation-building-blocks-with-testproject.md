# Creating automation building blocks with TestProject

Organizing and managing automated tests directly contributes to a successful test automation initiative. Test automation isn't a set it and forget it kind of activity. In order to have automated tests continue to add value they will need to be updated and changed as the product changes. A test suite that is designed with this in mind can continue to be valuable as time goes on. 

There are several strategies that can be used to help with this and one powerful strategy that can be used in TestProject, is breaking up tests into smaller pieces that can be shared. These building blocks make it much easier to update tests as they help organize your test actions and also consolidate common actions in one place. Another powerful strategy built into TestProject is the ability to setup and share parameters across tests. The also helps prevent duplication and allows you to make updates quickly and easily.

## Tests as Building Blocks

Let's take a look at these concepts by walking through setting up a test against the TestProject Demo site.

### Creating a Login Test

The first thing we need to do after navigating to the demo page is to login. Creating a test to do this is simple as setting up a project that uses the demo site url and then clicking on the name field and typing in a name and then similarly clicking on the password field and typing in the password. You can then click on the login button, and you will be taken to a sample page with a form you can fill out.

![Example Form After Login](../.gitbook/assets/image%20%2860%29.png)

If you have not yet set up a test in TestProject, you can find details on how to do that [here](../using-the-smart-test-recorder/web-testing/) in the documentation. 

### Creating a Valid Email Test

At this point though, imagine you want to create a few tests for this form. For example, perhaps you want to create a test that uses a valid email address and one that does not.

For each of these tests we will need to login. Rather than implement the login steps in each of the tests we can create one test for the login and then use that test in each of the other tests that we want to run. So if we go to the project where we have created this login test and we create a new test, we can remove the default Navigate to step

![Delete Step](../.gitbook/assets/image%20%28198%29.png)

We can now add a step and in the create step slide-out click on the Element action link in the Type section to change the step type.

![Change the Step Type](../.gitbook/assets/image%20%2813%29.png)

Set the step Type to Test and save the changes.

![Set Step Type to Test](../.gitbook/assets/image%20%28192%29.png)

You can then select the test you want and choose the Login test that you made earlier. Once you have added that test, click on Create to complete the creation of the test step.

![Select a test](../.gitbook/assets/image%20%2828%29.png)

Now, we can continue on with creating the rest of the test, but clicking on the record button.

![Record button](../.gitbook/assets/image%20%2888%29.png)

This will bring up the the TestProject recorder, and you can run the login step.

![Run Test Step](../.gitbook/assets/image%20%2857%29.png)

Once you have done this, you can write the rest of your test. So in this case, let's complete the filling out of the form with a valid email address. We can click on the Country dropdown and select the country we want, and then type in the address we want to use. Similarly, we can enter in the phone number and email address that we want to use and then click on the Save button. The TestProject recorder will add test steps for each of these actions. 

### Create Test Parameters

Now, we know that we want to create another similar test that uses a different email address, so we can parameterize the email field by clicking on that step.

![Email Test Step](../.gitbook/assets/image%20%28164%29.png)

In the step detail panel for this step we can then parameterize the input text that we are giving this field by clicking on the plus beside the field.

![Create a Parameter](../.gitbook/assets/image%20%2891%29.png)

On the parameters page that is brought up, you need to click on the new parameter plus button at the bottom left.

![Add new parameter](../.gitbook/assets/image%20%282%29.png)

Fill in the form for creating a parameter, giving it a name, and click on Add to complete the creation of the parameter.

![Add a new Parameter](../.gitbook/assets/image%20%2814%29.png)

Ensure that the new parameter you just created is now being used as the text for the email address test step, and save and apply all changes.

![Use the new Parameter](../.gitbook/assets/image%20%2868%29.png)

### Creating a Second Test

Now that the first test has been created you can make a second test with another email address. We will once again remove the default step as we did above and then add a step and change the type to test. We can then select a test, and in this case we will use the Valid Email test that we made above.

![Select Test](../.gitbook/assets/image%20%2823%29.png)

When choosing a test that has parameters, TestProject will prompt you asking if you would like to create the same parameters in the existing test. Choose yes to this prompt. We can then modify this parameter if we want by clicking on the plus icon beside the parameter.

![Go to Parameters](../.gitbook/assets/image%20%2886%29.png)

You can then modify the parameter using the edit icon.

![Modify Parameter](../.gitbook/assets/image%20%28176%29.png)

Parameters can also be managed at the project leve and controlled at run time, which make it easy to run and maintain test like this.

## Conclusion

In the scenario we have been thinking about we have created tests that build up on each other and this is a powerful way to make it easier to manage the tests in a test suite. With the example we created, we can imagine something changing on the login page. In that case we would just need to modify the one login test and all the test would be ok. If we hadn't set this up by building up parts of the test we would have needed to update each test that uses that code.

In this example we have demonstrated how this would work with recorded tests, but of course the same principles apply and can be put into effect with TestProject when working with coded tests as well. When it comes to managing your tests, the tools the TestProject offers make it straightforward to create and maintain tests that will be effective for as long as you need them.









