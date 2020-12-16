---
description: >-
  How to build automation scripts for web applications on mobile (iOS and
  Android)
---

# How To Record a Web Test for a Mobile Browser

## Why testing web applications on mobile?

The motivation for automating web tests on mobile is simple, in most cases our "regular" web site will look and behave differently while open on a mobile web browser, thanks to application responsive UI techniques developers are implementing. Most of the web applications will provide completely different functionality and in most cases will be changing their UI layout to provide "mobile-like" user experience \(the buttons changing their shapes, text become bigger,  UI elements become simplified, etc\).

 All that to fit gestures such as taps, swipes, and fit smaller screens. You can consider it as a completely new app you need to test.

Since TestProject utilizes selenium as a web driver and W3C there is no need to record a native mobile test \(which can be done with TestProject too\), a web test will do the job perfectly.

The idea will be creating a web test while keeping the mobile resolution during the recording session to force the application layout and the element to change just like they were recorded in mobile.

Then once the test is ready execute it on mobile iOS and Android. Let's see how it's done! 

## Creating a Web Test

First, we will create a simple Web Test  

1. Create a new Web Test.



![](../.gitbook/assets/image%20%28245%29.png)

2. Select Web.

![](../.gitbook/assets/image%20%28251%29.png)

3. Give the test a name and select the Web Application you wish to test and click on Record.

![](../.gitbook/assets/image%20%28253%29.png)

## Setting The Browser Settings To Simulate the Mobile Browser

To make sure we record a Web Test which will run well on the Mobile Device resolution, we need to change the recorder session window to Simulate the Mobile Browser resolution.

1. In the Recorder window, click on F12 to open Chrome Developer Tools.
2. In the Developer Tools Window, click on 'Toggle Device Toolbar'

![](../.gitbook/assets/image%20%28244%29.png)

The screen will then resize to a default resolution, we can adjust the resolution to be the one we need for the Specific devices we will be running the Test on.

By clicking on Responsive

![](../.gitbook/assets/image%20%28247%29.png)

You can select pre-defined Resolutions or you can input your own resolution.

We can see the Window will look like so:

![](../.gitbook/assets/image%20%28252%29.png)



We can go back to the Previous resolution and Resize the recorder Window:

![](../.gitbook/assets/image%20%28250%29.png)

## Recording The Test On Mobile Resolution

Now that we know how we can set the desired resolution for the Recorder session, we can just make sure we are on Recording Mode:

![](../.gitbook/assets/image%20%28248%29.png)

And we minimize the Recorder to get the application layout:

![](../.gitbook/assets/image%20%28242%29.png)



Now let's start interacting with the Web Application, the steps will be recorded and added automatically.

![](../.gitbook/assets/image%20%28243%29.png)

Once done, change the Resolution of the Recorder back to normal and reopen the minimized Recorder Menu



![](../.gitbook/assets/image%20%28254%29.png)

And we can see the steps were automatically added

![](../.gitbook/assets/image%20%28249%29.png)

We are now ready to execute the test on a Mobile device \(iOS or Android or Emulators\).

You can see how you can run a Web Test on a Mobile Browser [here](https://docs.testproject.io/tips-and-tricks/running-a-web-test-on-a-mobile-device)





