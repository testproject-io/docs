# Automatically Generate Code

The TestProject SDK makes it easy to create tests. If you have not used the SDK yet, you can find instructions on getting started with it in the [previous section](./). One of the cool things about TestProject is the close integrationd between the SDKs and the application. You don't have to create all your tests manually. You can actually use TestProject to generate your test code for you!

If you have not yet created tests using the TestProject recorder, you can find information on how to do that [here](../../../using-the-smart-test-recorder/web-testing/). Once you have created a test, you can easily generate code from that test using the following steps:

1. Login to the TestProject application and navigate to a test that you've made
2. On the menu beside the test choose the Generated Code option

![](../../../.gitbook/assets/image%20%28397%29.png)

This will bring up a dialog. TestProject will put a default name, but you can rename it to something else if you want. You can also select the SDK that you want \(in this case Java\) and ensure that the you have the OPenSDK V2 option selected. Pick the browser you want and then click on the Download button to download the code

![Download Code](../../../.gitbook/assets/image%20%28385%29.png)

{% hint style="info" %}
Note that some browsers will block a site from downloading, especially if you do multiple downloads. You may need to enable automatic downloading in your browser as shown in the image below.
{% endhint %}

![Enable Automatic Downloads](../../../.gitbook/assets/image%20%28395%29.png)

Once the code has downloaded, you can navigate to the file on your hard drive, and unzip it. It is now ready for you to use it!

## Using Generated Code

In this documentation we will show you how to use the generated code in Eclipse. If you are using a different IDE, you should be able to modify these steps to work for your IDE of choice. 

In Eclipse, open the **File** menu, and choose the **Import** option. On the import wizard, ensure that you have the **Existing Gradle Project** option selected and then click **Next**.

![Importing a Gradle Project](../../../.gitbook/assets/image%20%28391%29.png)

If you get the Gradle welcome page, click **Next** again and then use the **browse** button to browse to the folder that contians the files you unzipped. Select that folder and click **Finish** to complete the import. 

If you expand the `/src/test` folder you should be able to find the generated code in there.

![Generated Code File](../../../.gitbook/assets/image%20%28387%29.png)

You can now run this code or modify it as you see fit. This generated code can also be helpful for understand how the SDK works. 

