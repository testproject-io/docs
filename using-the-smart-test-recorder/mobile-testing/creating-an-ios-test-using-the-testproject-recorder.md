# Creating an iOS test using the TestProject Recorder

## Preparing for iOS Testing

You can record iOS tests in a live app from Windows using TestProject recording studio, but in order to do so you will need to setup a few things first. Make sure that you have followed the steps in the section of the documentation on [getting started with iOS testing from Windows](../../getting-started/getting-started-with-ios-testing-from-windows.md).

Once you have followed those steps you will be able to start creating iOS tests on any attached devices. 

## Creating a Test

Creating a new mobile test is as simple as clicking on the New Test button and then choosing the Mobile test option as your test type

![Add New Test](../../.gitbook/assets/image%20%285%29.png)

Once you have done that you can fill in a name and description for your test and press Next.  You will then need to select which platform and application you want to use. For recording on an iOS device you would choose the IOS platform and then you can select the app that you want to test.  If this is the first test you are creating for this device there will not be any applications in the list and so you will need to click on the Add a new application for testing button.

![Select Platform and Application](../../.gitbook/assets/image%20%2818%29.png)

## Adding an Application

You can add an application in a few different ways. A very simple way to do this is to make sure your device is connected and the agent is running and then selecting an application from the device. If you need to you can also manually add an application or just upload an IPA.

To select an application from your device, select it from the Device dropdown. The App dropdown will then be populated with all the apps on the device you have chosen and you can select the application you want to use from the list.

Once you have picked the application you want to use and given it a name you can click on Finish to select that application for the test you are creating.

## Recording a Test

Now that you have created your test and specified the application to use for testing, you are ready to start creating the steps that you want your test to execute.  You can create the steps manually if you want, or you can use the powerful recorder that TestProject offers

![Record a Test](../../.gitbook/assets/image%20%2828%29.png)

Choosing this will open the test recorder for you. The test recorder will show you the test steps and will also connect to your device and include a mirrored view of it with the application under test loaded up and ready for you to start testing.

![TestProject Recorder](../../.gitbook/assets/image%20%288%29.png)

During recording you can conveniently use the TestProject [Element Inspector](../finding-and-using-elements/element-inspector.md) and [Element Locator ](../finding-and-using-elements/element-locator.md)to verify your location strategies as you interact with your application through the mirrored view.

![Element Inspector and Locator](https://blog.testproject.io/wp-content/uploads/2018/06/iOS-Element-Locator-512x441.png)

Action that you perform on the mirror device will be added as steps in your test and you can quickly and easily build the test that you need. 

## Next Steps

If you want more details on how to select and use elements within the Recorder you can find information in the [finding and using elements](../finding-and-using-elements/) section of the documentation. If you want to see how to schedule and run the tests that you create you can find [information on that in the documentation as well](../../schedule-and-run-tests/create-and-schedule-jobs.md).

