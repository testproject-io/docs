# Creating an Android test using the TestProject Recorder

## Prepare your android device

Before you get started with recording tests on your android device, you will need to make sure it is in developer mode. You can do this by going to settings in your device \(for Android 8.0 and higher\) and then selecting the About \(sometimes called About Phone\) option.  Choose the Software Information option and then tap on the Build number option 7 times to enable developer mode.

Once you have done that you can find an option in the settings called developer options. You will need to choose that option and in there choose to enable the USB debugging option. Your device should now be ready to use with TestProject. Using an appropriate USB cable, you can plug it into any device with a TestProject agent in order to start using it. When you do that you should get a popup asking you to authorize the device for use with TestProject. Select yes on this and you can start creating your first Android test.

## Creating a Test

Creating a new mobile test is as simple as clicking on the New Test button and then choosing the Mobile test option as your test type

![Add a New Test](../../.gitbook/assets/image%20%28255%29%20%282%29.png)

Once you have done that you can fill in a name and description for your test and press Next.  You will then need to select which platform and application you want to use. For recording on an Android device you would choose the Android platform and then you can select the app that you want to test.  If this is the first test you are creating there will not be any applications in the list and so you will need to click on the Add a new application for testing button.

![Add a new Application](../../.gitbook/assets/image%20%28221%29.png)

## Adding an Application

You can add an application in a few different ways. A very simple way to do this is to make sure your device is connected and the agent is running and then selecting an application from the device. 

{% hint style="info" %}
If you do not see your device on the list, check that you have authorized it. You will need to approve USB debugging on your device. You can also check the Devices section on Agents tab to ensure that the device has been authorized to be used with TestProject. 
{% endhint %}

If you need to you can also manually add an application or just upload an APK. For this tutorial though, we will look at how to select an application from your device. Ensure that the application you want to test is installed on your device and then select your device from the dropdown.

![Choose a Device](../../.gitbook/assets/image%20%2876%29%20%281%29.png)

The App dropdown will then be populated with all the apps on the device you have chosen and you can select the application you want to use from the list. There is a search field that can be used to help you quickly find the application you are looking for.

![Select an Application](../../.gitbook/assets/image%20%2868%29.png)

Once you have picked the application you want to use and given it a name you can click on **Done** to select that application for the test you are creating.

## Recording a Test

Now that you have created your test and specified the application to use for testing, you are ready to start creating the steps that you want your test to execute. You can create the steps manually if you want, or you can use the powerful recorder that TestProject offers.

![Start Creating a Test](../../.gitbook/assets/image%20%28169%29%20%283%29%20%281%29.png)

You will also notice that you can choose to have the test files saved in the cloud, or saved to a local file. The **File**  option allows you to create tests that can be run offline. To learn more about the cloud versus offlines modes, check out the documentation [here](../../getting-started/hybrid-cloud-and-offline-mode/). 

When getting started, the best course of action is to use this test recorder. This will help walk you through the test steps and will also connect to your device and include a mirrored view of it with the application under test loaded up and ready for you to start testing. Simply choose the **Record** option and then click on **Start recording** to immediately get started.

### Creating Test Steps

In order to create test steps all you need to do is interact with the application in the emulator and each action will be recorded as a step in the test case. For example if you were testing the calculator app you could click on a number on the screen and that click would be recorded as a test step. 

![Actions recorded as Test Steps](../../.gitbook/assets/image%20%28261%29.png)

You can repeat that for each test step that you want to record, in order to quickly and easily build an entire test case. Once you have added the test steps that you want, you can add validation to your test by mousing over the element you want to validate and then hitting shift twice quickly \(Double Shift\). You can choose the validations option on the menu to add a validation step to your test

![Add a Validation Step](../../.gitbook/assets/image%20%28295%29.png)

After completing the test creation you can simply click on the **Save and Exit** button to save your changes and your test is ready to use!

![Save and Exit](../../.gitbook/assets/image%20%28138%29.png)

## Next Steps

If you want more details on how to select and use elements within the recorder you can find information in the [finding and using elements](../finding-and-using-elements/) section of the documentation. If you want to see how to schedule and run the tests that you create you can find [information on that in the documentation as well](../../schedule-and-run-tests/create-and-schedule-jobs.md).

