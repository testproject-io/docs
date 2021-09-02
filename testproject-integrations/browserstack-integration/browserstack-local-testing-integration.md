---
description: Running TestProject Tests & Jobs with Local Testing on BrowserStack Automate
---

# BrowserStack Local Testing Integration

**This guide shows you how to set up and run TestProject tests on BrowserStack Local Testing for both Recorded and Coded Tests.**

## What is Local Testing on BrowserStack Automate?

Local Testing on BrowserStack will let you test your applications hosted on your local computer \("localhost"\) or behind a corporate firewall, hosted in development or testing environments.

## When is BrowserStack Local Necessary?

In order for BrowserStack to be able to test your in-house/non-public tests, and make it accessible for BrowserStack’s servers, a tunnel should be opened between your machine to BrowserStack. If you will try to test your in-house/non-public tests on BrowserStack, your test will fail, due to ERR\_CONNECTION\_REFUSED, your app will not be accessible.

![](../../.gitbook/assets/image%20%28149%29%20%281%29.png)

## Execute TestProject Recorded Tests on Local Resources via BrowserStack

### Requirements

1. [**TestProject**](https://testproject.io/) **account:** you will need an active TestProject account. If you don't already have one, you can [sign up](https://app.testproject.io/signup/) for a free forever account [here](https://app.testproject.io/signup/).
2. **Connect BrowserStack with TestProject as** **explained** [here](https://docs.testproject.io/testproject-integrations/browserstack-integration#setting-up-browserstack-integration).

To use BrowserStack with local resources you need to download **BrowserStackLocal** **binary**:

* [OS X \(10.7 and above\)](https://www.browserstack.com/browserstack-local/BrowserStackLocal-darwin-x64.zip)
* [Linux 32-bit](https://www.browserstack.com/browserstack-local/BrowserStackLocal-linux-ia32.zip)
* [Linux 64-bit](https://www.browserstack.com/browserstack-local/BrowserStackLocal-linux-x64.zip) 
* [Windows \(XP and above\)](https://www.browserstack.com/browserstack-local/BrowserStackLocal-win32.zip)

### **Get** **Your BrowserStack** **Access Key** **& Run it with the BrowserStack Binary**

BrowserStack Access Key can be found under your account in the “Settings” section [https://www.browserstack.com/accounts/settings](https://www.browserstack.com/accounts/settings).

Copy your access key to clipboard, open CMD/Terminal in the folder where BrowserStackLocal binary is located in your machine, run the following command according to your operating system:

OS X & Linux:

```text
./BrowserStackLocal --key {YOUR_ACCESS_KEY}
```

Windows:

```text
BrowserStackLocal.exe --key {YOUR_ACCESS_KEY}
```

Expected output:

![](../../.gitbook/assets/image%20%28144%29.png)

## **Execute recorded tests by TestProject on remote Browserstack cloud**

1. First, we need to create a recorded test, in this example, we will use a web test
2. Create a job and assign the desired tests– a job is a tool to aggregate, manage, schedule and run    tests
3. Set desired capability

*  Create a job by clicking on “New Job” button

![](../../.gitbook/assets/image%20%28138%29%20%282%29%20%282%29%20%281%29%20%282%29%20%282%29%20%282%29.png)

* Configure your job to execute assigned tests on BrowserStack remote browsers, Drag and Drop the required tests into it. For example:

![](../../.gitbook/assets/image%20%28131%29.png)

* Set a Desired Capability to this job, that will activate the connection with BrowserStack and enable access to your app. ![](file:///C:/Users/TESTPR~1/AppData/Local/Temp/msohtmlclip1/01/clip_image006.jpg)

        Set **browserstack.local** capability to true by adding the following:

![](../../.gitbook/assets/image%20%28152%29.png)

You are all set to run your job.

## Run Coded Tests on Local Resources with BrowserStack Cloud and TestProject OpenSDK

**Configure Remote \(Cloud\) Driver to BrowserStack**

By default, TestProject Agent communicates with the local Selenium drivers or Appium server that are bundled within the agent application, then send automatic execution reports to TestProject Dashboard.

A basic example of running Selenium tests on remote BrowserStack servers by utilizing TestProject’s Agent:

```text
import io.testproject.sdk.drivers.TestProjectCapabilityType;
import io.testproject.sdk.drivers.web.ChromeDriver;
import org.openqa.selenium.chrome.ChromeOptions;


String AUTOMATE_USERNAME = "{BS_USERNAME}";
String AUTOMATE_ACCESS_KEY = "{BS_ACCESS_KEY}";
String URL = "https://" + AUTOMATE_USERNAME + ":" + AUTOMATE_ACCESS_KEY + "@hub-cloud.browserstack.com/wd/hub";


ChromeOptions chromeOptions = new ChromeOptions();
chromeOptions.setCapability(TestProjectCapabilityType.CLOUD_URL,URL);


ChromeDriver driver = new ChromeDriver(chromeOptions);
```

**There are two different ways to establish a Local Testing connection:**

**1. Within your code**, using browsetstack-local dependency 

#### **Java –** \(available in maven-center\)

Gradle:

```text
compile group: 'com.browserstack', name: 'browserstack-local-java', version: '1.0.3'
```

Maven:

```text
<dependency>
    <groupId>com.browserstack</groupId>
    <artifactId>browserstack-local-java</artifactId>
    <version>1.0.3</version>
</dependency>
```

#### **Python -**

```text
pip install browserstack-local
```

**2. By running BroswerStack Local binary** via command-line interface as mentioned in[ “**Get** **Your BrowserStack** **Access Key** **& Run it with the BrowserStack Binary**”](https://docs.testproject.io/testproject-integrations/browserstack-integration/browserstack-local-testing-integration#get-your-browserstack-access-key-and-run-it-with-the-browserstack-binary) guide above.

\*\*\*\*

**Within your code:**

Integrate your code with the following to establish the ****BrowserStack Local connection:

```text
import com.browserstack.local.Local;


Local bsLocal = new Local();
HashMap<String, String> bsLocalArgs = new HashMap<String, String>();
bsLocalArgs.put("key", {BS_ACCESS_KEY});
bsLocal.start(bsLocalArgs);
bsLocal.stop();
```

After establishing the Local Testing connection, set **browserstack.local** capability to true in driver’s desired capabilities:

```text
setCapability("browserstack.local", "true");
```

### TestProject Java OpenSDK example for cross-platform testing on an app hosted in localhost using BrowserStack local:

```text
import com.browserstack.local.Local;
import io.testproject.sdk.drivers.TestProjectCapabilityType;
import io.testproject.sdk.drivers.web.ChromeDriver;
import org.openqa.selenium.By;
import org.openqa.selenium.Platform;
import org.openqa.selenium.chrome.ChromeOptions;
import org.openqa.selenium.remote.CapabilityType;
import java.util.HashMap;

public final class WebTest {


  public static void main(final String[] args) throws Exception {

    // perparing URL for remote driver
    String AUTOMATE_USERNAME = "{BS_USERNAME}";
    String AUTOMATE_ACCESS_KEY = "{BS_ACCESS_KEY}";
    String URL = "https://" + AUTOMATE_USERNAME + ":" + AUTOMATE_ACCESS_KEY + "@hub-cloud.browserstack.com/wd/hub";

    // creating an instance of Local and starting it

    Local bsLocal = new Local();
    HashMap<String, String> bsLocalArgs = new HashMap<String, String>();
    bsLocalArgs.put("key", AUTOMATE_ACCESS_KEY);
    bsLocal.start(bsLocalArgs);

    Platform[] platforms = {Platform.MAC, Platform.WINDOWS, Platform.WIN8};
    for(Platform platform : platforms) {

        // setting up driver

        ChromeOptions chromeOptions = new ChromeOptions();
        chromeOptions.setCapability(
                TestProjectCapabilityType.CLOUD_URL, URL);
        chromeOptions.setCapability("browserstack.local", "true");
        chromeOptions.setCapability(CapabilityType.PLATFORM_NAME, platform);
        ChromeDriver driver = new ChromeDriver("{TP_DEV_TOKEN}", chromeOptions, "BS Local Examples");

        driver.navigate().to("http://localhost:3000");

        boolean passed = driver.findElement(By.cssSelector("#app-title")).isDisplayed();

        if (passed) {
            System.out.println("Test Passed");
        } else {
            System.out.println("Test Failed");
        }
        driver.quit();
        }

        // stopping Local instance
        bsLocal.stop();

    }

}
```

\*\*\*\*

**By running BroswerStack Local binary:**

As mentioned in [Get Your BrowserStack Access Key & Run BrowserStack Binary](https://docs.testproject.io/testproject-integrations/browserstack-integration/browserstack-local-testing-integration#get-your-browserstack-access-key-and-run-it-with-the-browserstack-binary) you can easily run BroswerStack Local binary via command-line interface, and only set **browserstack.local** capability to true in driver’s desired capabilities:

```text
setCapability("browserstack.local", "true");
```

{% hint style="info" %}
It is important to note - BrowserStack Local binary should be up and running while executing the coded test
{% endhint %}

### TestProject Python OpenSDK example for cross-browsers testing on an app hosted in localhost using BrowserStack local:

```text
from selenium.webdriver import DesiredCapabilities
from src.testproject.sdk.drivers import webdriver

def simple_test():

    broswercaps = [DesiredCapabilities.FIREFOX.copy(), DesiredCapabilities.CHROME.copy(), DesiredCapabilities.SAFARI.copy()]

    for caps in broswercaps:

        caps["cloud:URL"] = "https://" + "{BS_USERNAME}" + ":" + "{BS_ACCESS_KEY}" + "@hub-cloud.browserstack.com/wd/hub"
        caps["browserstack.local"] = "true"
        driver = webdriver.Remote(token="{TP_DEV_TOKEN}", desired_capabilities=caps)
        driver.get("http://localhost:3000")
        passed = driver.find_element_by_css_selector("#app-title").is_displayed()
        print("Test passed") if passed else print("Test failed")
        driver.quit()

if __name__ == "__main__":

    simple_test()
```

## **Execution Test Reports**

Once your recorded/coded test execution has been completed, you can hop over to the [Reports](https://app.testproject.io/#/reports) section in your TestProject account to see the results of your test\(s\).

![](../../.gitbook/assets/image%20%28151%29.png)

### **BrowserStack** **test execution information**

Once you click the Open BrowserStack report link, you will be redirected to BrowserStack where you will be able to see that your website \(that is not publicly accessible\) has been reached, with some additional information about that execution:

![](../../.gitbook/assets/image%20%28133%29.png)

