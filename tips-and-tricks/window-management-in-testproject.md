# Window Management in TestProject

Many modern websites are built with responsive designs meaning they will automatically adjust the elements to display correctly with different sized screens. This is a powerful and very helpful design paradigm that helps websites to be useful across a wide variety of devices and screens. However, it can be a difficult thing from a testing perspective. Unless you have a large variety of devices of different sizes it can be difficult to ensure that your site will be properly responsive at different sizes.

The [Web Extensions Addon ](../testproject-addons/available-addons/web-extensions-addon.md)in TestProject provides a number of very useful actions. Some of those actions can allow us to solve the problem of testing across different sized screens. There are actions that allow you to set the size of the current window and also to switch between windows or tabs and even to move a window around on the screen. Let's take a look at an example of how you could use these actions in a test. 

## Getting Started

If you have not yet created a test, you can follow the instructions in on [creating a web test](../using-the-smart-test-recorder/web-testing/creating-a-web-test-using-the-testproject-recorder.md) to get setup. For this example, we will use the TestProject landing page since is has a nice responsive design. Once you have a test setup that is pointing to [https://testproject.io/](https://testproject.io/) start the test recorder and we can get going

## Resizing

The first thing we will do in this test is create a test step to resize the window. You can add a new test step using the plus button at the bottom of the panel, and then change the step type to action. 

![Change step type to Action](../.gitbook/assets/image%20%28147%29.png)

You can then click on the select action link and search for `window`. In the resulting list, select the `Set window size` action. With this action you can set the both the width and the height that you want the window to have. Put in values of something like 1000 and 600 and save the test step. Click the arrow beside the test step and run it.

![Run the Test Step](../.gitbook/assets/image%20%2864%29.png)

This will run the test step and resize the window for you.

## Different sizes with Parameters

At this point we could create the rest of the test steps to ensure that elements on the page have resized appropriately, but all we had done so far is test out one size. What if there were several different size screens that we wanted to test? We could make all of our test steps, resize the screen and then make all the same test steps again. This would require a lot of repetition and not be very nice to make and maintain. Thankfully TestProject has a powerful feature we can use here: parameters.

If you go to the test step you can click on the plus button beside the input parameters to parameterize them.

![Parameterize Button](../.gitbook/assets/image%20%28134%29.png)

This will bring up the parameters panel.Clear the Width field and then click on the plus to add a new parameter

![Add new parameter](../.gitbook/assets/image%20%2846%29.png)

Name the parameter something like `WindowWidth` and give a value of 100 and then click on Add. This will create a new parameter and put it in the Width field. Click on the green check mark to save it. 

![Save Parameter](../.gitbook/assets/image%20%2852%29.png)

Repeat the same process to add a `WindowHeight` parameter to the height field and then save the test step.

## Create Multiple Window Size Values

Now that we have the width and height parameterized, let's look at how we can drive this test with multiple values for those parameters. Close the test recorder and go to the page for the project that has the test you are creating. Click on the `more` menu beside the test and choose the Data Source Template option 

![Download a Data Source Template](../.gitbook/assets/image%20%2861%29.png)

This will download a `.csv` file for you. Open that file. You can remove the  ApplicationURL column since we don't want to change that. Then create values that looks something like this.

![Window Sizes](../.gitbook/assets/image%20%288%29.png)

{% hint style="info" %}
Note that the column names \(in this example WindowWidth and WindowHeight\) should match the names of the parameters you made in the test.
{% endhint %}

Click on the Data Sources tab in the left hand navigation and then click on the Add a new Data Source button.

![Add a new Data source](../.gitbook/assets/image%20%28159%29.png)

Choose the `.csv` file you just created and name the data source something like `WindowSizes.`Now go back to the tests and click on the run button beside the test you are working on.

![Run Test](../.gitbook/assets/image%20%28126%29.png)

On the resulting popup, choose the browser you want to run the test on and then click Next.  Now choose the `Use data source` option and select the data source you just created.

![Use Window Sizes data source](../.gitbook/assets/image%20%28213%29.png)

Run the test and you will notice that the test is run once for each of the window sizes that you specified in the `.csv` file.

## Conclusion

One of the many useful addon actions that TestProject has is the ability to resize windows. When combined with parameters and data driven testing, this action can help you simulate testing on many different screen sizes all in one test. 

