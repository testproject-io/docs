---
description: >-
  A collection of useful scripts for mobile setup while working with TestProject
  Python OpenSDK
---

# Mobile Scripts Python OpenSDK

## Prerequisites

Before using some of the below methods, we will need to obtain an API key, agent ID and device UDID which are all can be extracted from TestProject UI, no worries it really simple.

1. Navigate to TestProject API Page: [https://app.testproject.io/#/integrations/api](https://app.testproject.io/#/integrations/api), get your API Key, or create one if you do not have one.

![](<../../.gitbook/assets/image (293).png>)

&#x20;  3\. In the Agents tab, press on the desired agent, devices and copy the UDID, read more about how to do it [here](https://docs.testproject.io/tips-and-tricks/finding-device-udid).

&#x20;  4\. Copy the Agent ID which you can find on the Agents page [here](https://app.testproject.io/#/agents).

![](<../../.gitbook/assets/image (292).png>)

## Get a list of connected mobile devices

The bellow Python script will get the agent connected devices based on agent ID. Make sure to supply the API key and Agent ID which you obtained as described before.&#x20;

```
import requests as req

api_key = ""  # Your API Key, which you get from TestProject UI https://app.testproject.io/#/integrations/api
agent_id = ""  # The Agent ID which you also retrieve from the TestProject UI https://app.testproject.io/#/agents
base = f"https://api.testproject.io/v2"


def get_agent_devices():
    data = {"Authorization": api_key}
    res = req.get(url=f"{base}/agents/{agent_id}/devices", headers=data)
    print(res.status_code, res.text)


if __name__ == '__main__':
    get_agent_devices()
```

## Get agent state

The agent can be in 5 different states: Disconnected, Idle, Development, Recording, Executing. to start your CI the agent should be in **Ready** state. Use the below Python script for validating the agent state.&#x20;

```
import requests as req

api_key = ""  # Your API Key, which you get from TestProject UI https://app.testproject.io/#/integrations/api
agent_id = ""  # The Agent ID which you also retrieve from the TestProject UI https://app.testproject.io/#/agents
base = f"https://api.testproject.io/v2"


def get_agent_state():
    data = {"Authorization": api_key}
    res = req.get(url=f"{base}/agents/{agent_id}/state", headers=data)
    print(res.status_code, res.text)


if __name__ == '__main__':
    get_agent_state()

```

## Get installed applications

Below is the Python code to query the agent API to get the installed applications on the connected device. The response will be a JSON array of all installed applications on the device selected.

```
import requests as req

port = "8585"  # This is the feault Agent communication port
base = f"http://localhost:{port}"
udid = ""  # UDID of the device to pull the apps from


def get_list_of_installed_applications():
    res = req.get(url=f"{base}/api/devices/{udid}/apps")
    print(res.status_code, res.text)


if __name__ == '__main__':
    get_list_of_installed_applications()
    
```

## Installing an APK/IPA in Runtime with OpenSDK&#x20;

TestProject takes care of IPA/APK installations and deployment process out of the box when using recorded tests or when uploading the code binaries to TestProject cloud. If you prefer to use a local CI with the OpenSDK, the process to install an IPA/APK programmatically on a device in Runtime will be the same as using fluent Appium commands.  The below Python script will deploy and install locally saved APK/IPA on the connected device and execute the example test script.&#x20;

You can reinstall the application if the 'noReset' capability is provided with the value of 'true'.

Prerequisites: TestProject agent is installed, registered and in Ready state, the latest version of TestProject OpenSDK is installed, developer key is provided (can be obtained from the [integration ](https://app.testproject.io/#/integrations/sdk)area as described above).



{% hint style="info" %}
If no token is provided in the constructor of the driver, it will use the environment variable TP\__DEV\_TOKEN_
{% endhint %}



```
from selenium.webdriver.common.by import By
```

```
from src.testproject.sdk.drivers import webdriver
import pytest


@pytest.fixture
def driver():

    device_udid = "emulator-5554"  # This is the Device UDID
    desired_capabilities = {
        "app": "C:\\Test\\testproject-demo-app.apk",
        "udid": device_udid,
        "platformName": "Android",  # You can change this to IOS if you are installing an IPA
        "fullReset": "true",
    }

    #  Replace 'token' with your developer token https://app.testproject.io/#/integrations/sdk
    driver = webdriver.Remote(token="kJCeheorpsyq8u4Z17k0JQyBck1qLIf5ZrynbI6t7Fk1", desired_capabilities=desired_capabilities)

    yield driver

    driver.close_app()
    driver.quit()


#  This simple test will install the TestProject application inside the path above and run those simple steps.
#  It will re install the app using the fullReset capability.
def test_install(driver):
    textfield_name = (By.ID, "name")
    textfield_password = (By.ID, "password")
    button_dologin = (By.ID, "login")

    username = "TestProject"
    password = "12345"

    driver.find_element(*textfield_name).send_keys(username)
    driver.find_element(*textfield_password).send_keys(password)
    driver.find_element(*button_dologin).click()


```

{% hint style="info" %}
You can also install an IPA for an IOS device by changing the 'platformName' to IOS.
{% endhint %}
