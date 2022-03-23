---
description: Run TestProject Tests & Jobs on a Sauce Labs proxy tunnel
---

# Sauce Labs Proxy Tunnel Integration

## **What is** **a** **Sauce Labs proxy tunnel?**

Sauce Connect Proxy is a built-in HTTP proxy server that opens a secure "tunnel" connection for testing between a Sauce Labs virtual machine or real device and a web app hosted on your local computer ("localhost") or behind a corporate firewall. It provides a means for Sauce Labs to access your web application.&#x20;

## **When is Sauce Connect Proxy Necessary?**

**Sauce Connect Proxy** is required in situations when you run your tests/jobs in TestProject on a web app being tested using Sauce Labs which is on a private network and not publicly accessible. If you will try to test a web app hosted on your local computer ("localhost") or behind a corporate firewall using Sauce Labs, your test will fail, due to this error message:

![](<../../.gitbook/assets/1 (1).png>)

Setting Up Sauce Labs proxy tunnel Integration
----------------------------------------------

### Requirements

* [**TestProject**](https://testproject.io) **account** - In order to enjoy all the features of the TestProject platform, you will need an active TestProject account. If you don't already have one, you can [sign up](https://app.testproject.io/signup/) for a free account [here](https://app.testproject.io/signup/).
* [**Sauce Labs**](https://saucelabs.com) **account** - To utilize Sauce Labs cloud you need an account. If you don't already have one, just visit [here](https://saucelabs.com/sign-up) to create a free trial.
* Download **Sauce Connect Proxy.**
* Open outbound **port 443** in your machine

### **Get Sauce Labs Username & Access Key**

In order to setup the integration, you will have to obtain a Sauce Labs Access key. After logging into your Sauce Labs account, visit the [setting area](https://app.saucelabs.com/user-settings) (1-2) and copy your **User Name (3)** and **Access Key (4)**.

![](<../../.gitbook/assets/2 (1).png>)

### &#xD;**Download Latest Version of Sauce Connect Proxy**

Under your Sauce Labs account, navigate to TUNNELS tab and get the latest Sauce Connect Proxy for you operating system.

![](<../../.gitbook/assets/3 (2).png>)

### &#xD;**Open outbound port 443 in your machine**

In order to enable Sauce Connect Proxy to listen to Selenium commands, we will need to open this port on our machine.

Here’s an example for window 10: Open your Windows Defender Firewall:

![](<../../.gitbook/assets/4 (2).png>)

![](<../../.gitbook/assets/5 (2).png>)

![](<../../.gitbook/assets/6 (2).png>)

![](<../../.gitbook/assets/7 (2).png>)

![](<../../.gitbook/assets/8 (1).png>)

![](<../../.gitbook/assets/9 (1).png>)

### &#xD;**Configure Sauce Connect Proxy**

After extracting the downloaded Sauce Connect Proxy, go to the install directory and run:

![](<../../.gitbook/assets/10 (1).png>)

You can also copy an already generated command for you in the Sauce Labs UI under the TUNNELS tab:

![](<../../.gitbook/assets/11 (1).png>)

Copy/paste and run it using a CMD or a Terminal:

![](<../../.gitbook/assets/12 (1).png>)

When you see `Sauce Connect is up, you may start your tests.`, go to **Tunnels**, in Sauce Labs UI after you logged in to your account, Under **Active Tunnels**, you should see the tunnel you've just started.

![](<../../.gitbook/assets/13 (1).png>)

![](../../.gitbook/assets/14.png)

Run Recorded Tests from TestProject Platform
--------------------------------------------

TestProject's Agent supports running tests both locally on-premise, and on the cloud. Therefore, you can test private (local) web sites or access local resources such as databases, local directories, APIs, etc.&#x20;

What happens if you want to achieve the same functionality while utilizing the TestProject virtual agent, executing tests on remote Sauce Labs environments? You can achieve that with TestProject! All you need to do is enable the desired capability while executing your job, according to the following steps:

* Create a new job by clicking on "Add a new job" button:

![](../../.gitbook/assets/job.png)

* Drag and drop your test into the job, and configure your job to execute on Sauce Labs:

![](../../.gitbook/assets/sauce-labs.png)

* Set the desired capability to this job, that will active the tunnel and enable access to your app:

![](../../.gitbook/assets/desired-capabilities.png)

{% hint style="info" %}
You can find a tunnel's Name under the "Tunnels" section in your Sauce Labs account.
{% endhint %}

![](<../../.gitbook/assets/image (384).png>)

## Run Coded Tests using TestProject OpenSDK

### **Configure Remote (Cloud) Driver to your Sauce Labs proxy tunnel**

By default, TestProject Agent communicates with the local Selenium drivers or Appium server that are bundled within the agent application, then send automatic execution reports to TestProject Dashboard In order to initialize a remote driver for a Sauce Labs proxy tunnel, a custom capability “cloud:URL” and a “tunnelIndetifier” with a given tunnel name should be set.

A basic example of running Selenium tests on remote Sauce Labs servers by utilizing TestProject’s Agent:

```
import io.testproject.sdk.drivers.web.ChromeDriver;
import io.testproject.sdk.drivers.TestProjectCapabilityType;

ChromeOptions chromeOptions = new ChromeOptions();
chromeOptions.setCapability(
        TestProjectCapabilityType.CLOUD_URL,
        "https://{USERNAME}:{PASSWORD}@ondemand.us-west-1.saucelabs.com:443/wd/hub");
chromeOptions.setCapability(“tunnelIdentifier”, “{tunnelName}”)”
ChromeDriver driver = new ChromeDriver(chromeOptions);
```

### &#xD;**TestProject Java OpenSDK example for running a test on Windows 10 using multiple browsers:**

```
import io.testproject.sdk.drivers.TestProjectCapabilityType;
import io.testproject.sdk.drivers.web.RemoteWebDriver;
import org.openqa.selenium.By;
import org.openqa.selenium.Platform;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.remote.DesiredCapabilities;


public final class WebTest {


    public static void main(final String[] args) throws Exception {


        RemoteWebDriver driver;


        DesiredCapabilities[] browsers = {DesiredCapabilities.firefox(),DesiredCapabilities.chrome(),DesiredCapabilities.internetExplorer()};
        for(DesiredCapabilities browser : browsers){
            browser.setCapability(
                TestProjectCapabilityType.CLOUD_URL,
                "https://Meidan:46b57ewefwea7-e260-43ed-bd37-3aff0943bf45@ondemand.eu-central-1.saucelabs.com:443/wd/hub");
            browser.setCapability("tunnelIdentifier", "TPtunnel");
            browser.setPlatform(Platform.WIN10);
            driver = new RemoteWebDriver("aUV7b3u1F9Bwef5Ze2Dwq63xc8BQj6btBhNj-Lr2HzReiw1", browser );
            driver.navigate().to("http://localhost:3000");

            String s = driver.findElement(By.className("App-header")).getText();

            boolean passed = s.contains("Test Automation");
            if (passed) {
                System.out.println("Test Passed");
            } else {
                System.out.println("Test Failed");
            }

            driver.quit();
        }
    }
}
```

### &#xD;**TestProject Python OpenSDK example for running a test on multiple Operation Systems using Chrome:**

```
from src.testproject.sdk.drivers import webdriver
from src.testproject.sdk.drivers.webdriver.chrome import ChromeOptions

def simple_test():
    platforms = ['WINDOWS', 'MAC', 'LINUX']
    for platform in platforms:
        chrome_options = ChromeOptions()
        chrome_options.set_capability("cloud:URL", "https://Meidan:46b57ea7-e260-43ed-bd37-3aff0943bf45@ondemand.eu-central-1.saucelabs.com:443/wd/hub")
        chrome_options.set_capability("tunnelIdentifier", "TP_Proxy_Tunnel")
        chrome_options.set_capability('platform', platform)
        driver = webdriver.Chrome(token="aUV7b3u1F9B5Ze2Dwq63xc8BQj6btBhNj-Lr2HzReiw1", chrome_options=chrome_options)
        driver.get("http://localhost:3000")
        a = driver.find_element_by_class_name("App-header").text
        passed = "Test Automation" in a
        print("Test passed") if passed else print("Test failed")
        driver.quit()

if __name__ == "__main__":
    simple_test()
```

When you run your coded test locally on your machine, your web app that is not publicly accessible will be reached by your Proxy tunnel, and test reports will be generated automatically to TestProject platform.

## **Execution Test Reports**

Once your coded test execution has been completed, you can hop over to the [Reports](https://app.testproject.io/#/reports) section in your TestProject account to see the results of your test(s).

![](../../.gitbook/assets/15.png)

### &#xD;**Sauce Labs test execution information**

Once you click the Open Sauce Labs report link, you will be redirected to Sauce Labs where you will be able to see that your website (that is not publicly accessible) has been reached, with some additional information about that execution:

![](../../.gitbook/assets/16.png)
