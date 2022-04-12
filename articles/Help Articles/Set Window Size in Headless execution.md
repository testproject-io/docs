---
description: >-
  In this article we will learn how to set window size during headless execution
  with coded tests as well as by utilizing the Smart Recorder.
---

# Set Window Size in Headless execution

### Set window size by utilizing Smart Test Recorder <a href="#set-window-size-by-utilizing-smart-test-recorder" id="set-window-size-by-utilizing-smart-test-recorder"></a>

To set the screen size during headless execution by utilizing the test recorder, you need to have the **Web Extensions** addon and look for Set windows size action.\
You can find it here: [https://addons.testproject.io/web-extensions](https://addons.testproject.io/web-extensions).\
\
After the first step of "Navigate to" action add a step of "Set window size"

![](../../.gitbook/assets/chrome\_cRScbKPpYC.png)

Then, select the Set Window Size and supply the required size.

For example:

![](../../.gitbook/assets/chrome\_A5VII9jLD2.png)

\
You can also use the **Maximize Screen** action if you wish it to run on full screen.

That's it, now you run your test in headless mode with the desired solution!&#x20;

### Set window size with Coded Test <a href="#set-window-size-with-coded-test" id="set-window-size-with-coded-test"></a>

In your coded test you can easily change the window size by using the driver instance.

```java
// We get the instance for the web driver
WebDriver driver = helper.getDriver(); 

// set the window to the dimension we want, for example 1440, 900
driver.manage().window().setSize(new Dimension(1440, 900));

// With this line we can set it to full screen
driver.manage().window().fullscreen();
```

### &#x20;Cloud Environments <a href="#h_02c89d04c2" id="h_02c89d04c2"></a>

#### BrowserStack <a href="#h_66a50686f3" id="h_66a50686f3"></a>

For BrowserStack you will need to provide a custom capability as described here:

[https://www.browserstack.com/docs/automate/selenium/change-screen-resolution](https://www.browserstack.com/docs/automate/selenium/change-screen-resolution)

Into the Job:

![](https://downloads.intercomcdn.com/i/o/352242992/d5b4b0e0b96a86b09a79e134/Screen+Shot+2021-06-18+at+11.29.37.png)

```json
{
  "resolution": "1920x1080"
}
```

Like this:

![](https://downloads.intercomcdn.com/i/o/352243227/06ce05e603ae8562ba522e15/Screen+Shot+2021-06-18+at+11.32.42.png)

Happy testing!

\
