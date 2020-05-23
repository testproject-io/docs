# Using Natural Language Commands to Run a Test

The TestProject recorder makes it easy to create new tests. If you open the recorder and interact with the application, TestProject will record your actions into test steps that you can play back later. This is a great way to get started with writing test automation without needing to know any programming, but sometimes the test steps that get created can be a big fragile to change. For example, if a test step use xpath commands to find the element, it might break if the element is moved to another spot on the page. 

The [Natural Language Processing Engine Addon](../testproject-addons/available-addons/natural-language-processing-engine-addon.md) can help with this. This addon lets you enter commands in "plain English" sentences which it then parse to figure out what actions you want to do and what element you want to do that action on. Since you are specifying the element in 'natural language' terms and not in terms of something like an xpath, these kinds of command can be a bit more robust to minor changes in the page layout. Let's look at an example to see what it would look like to use these commands

## Getting Started

If you have not yet created a test, you can follow the instructions in on [creating a web test](../using-the-smart-test-recorder/web-testing/creating-a-web-test-using-the-testproject-recorder.md) to get setup. For this example, we will use the TestProject forum login page. We won't actually log into it with the test, but we will look at how you can fill out the login form with and without using the natural language processing engine. Once you have a test setup that is pointing to [https://forum.testproject.io/](https://forum.testproject.io/) start the test recorder and we can get going.

## Recording the Steps Directly

Let's first look at creating the test steps the way we usually would.  First we will click on the Login button at the top of the page.

![Login Button](../.gitbook/assets/image%20%28206%29.png)

This adds a step to the test, called `Click Login <span>.` If you click on that test step and look at it you can see that it has found the element using an XPATH locator

![Found using XPATH](../.gitbook/assets/image%20%28180%29.png)

This is fine for now, but if this page was ever redesigned and the login button was moved elsewhere on the page this test step would not be able to find the element and would time out. For now let's keep going with the test and fill in the username and password fields. After clicking in the username field and typing in an email address and typing a \(fake\) password into the password field, your test steps should look something like this:

![Test Steps](../.gitbook/assets/image%20%2867%29.png)

This is a nice enough test, but let's a take a look at how we could do it with the natural language processing engine instead.

## Using the NLP Engine

Close the test recorder and create a new web test that also points to [https://forum.testproject.io/](https://forum.testproject.io/) and start the test recorder for that test.

This time instead of just clicking on the elements we are going to add test steps. Use the plus button at the bottom of the test steps page to create a new test step. Change the Type to Action and click the check mark to apply the changes.

![Add an Action Test Step](../.gitbook/assets/image%20%2875%29.png)

You can now click on the Select Action link and search for NLP. Click on the `Run NLP Command`action. In the sentence field type `Click Login Button`This will click on login button, but in this case it does not use the xpath, so if the button was to move to another location on the page this test step would continue to work.

Now add another test step using the `Run NLP Command` and this time type in the text `Enter bob@example.com into username` This will type the email address into the username field. Similarly create a NLP test step that  has the sentence  `Enter 12345 into password` to type in the password field.  Your test should now look something like this:

![Test With NLP Commands](../.gitbook/assets/image%20%2812%29.png)

As you can see when comparing this test to the previous one, not only does the login button have more resilience to change, but you were also able to combine two steps into one when entering text in the form fields. 

## Conclusion

Sometimes the quickest and easiest thing to do when creating a test is to directly interact with the page and let the test recorder automatically record all actions. Other times, when we might care about stability or conciseness the Natural Language Processing Engine might give you commands that help you. TestProject really is a flexible and robust platform that gives you multiple ways to do things that meet the many different needs of testers. 

