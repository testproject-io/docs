# Troubleshooting DevToolsActivePort file doesn't exists

The recorder is crashing with the error Operation failed please try again.

In the agent logs you can see the error message `Caused by: org.openqa.selenium.WebDriverException: unknown error: Chrome failed to start: crashed. (unknown error: DevToolsActivePort file doesn't exist)`

The Agent logs can be found in the Agents tab > click on the 3 dots in you agent bar > download logs. [See gif](https://downloads.intercomcdn.com/i/o/148685195/28ed8bab622f67fe3d364baf/FkjHUZVhLW.gif).

This can happen in several scenarios:

**Chrome version mismatch**

TestProjects support Chrome versions 77 and newer, make sure the Chrome version installed on your machine (including other users) is suitable. You can find the Chrome version by navigating to`chrome://version/` in the browser and looking at the first line &#x20;

![](<../.gitbook/assets/image (227) (1) (1) (1).png>)

To update Chrome go to the 3 dots next to the profile icon on the top toolbar > help > About Google Chrome

![](<../.gitbook/assets/image-1- (3) (3) (3) (2) (3) (3).png>)

**Running Agent as administrator**

The Agent is running as administrator. Running and installing the Agent should be as regular user, not as administrator.

**Missing debug configuration for Windows**

If the above options didn't solve the issue go to `C:\Users\<username>\AppData\Roaming\TestProject\Agent` and add a file called` debug-configuration.json` with the content

`{ "tp.config.chrome.no.sandbox" : "true" }`

**Antivirus is blocking the recorder and tests**

In case you are using Quick Heal antivirus you need to disable browser sandbox. Open Quick Heal Total Security dashboard and go to Protection and select Browser Sandbox

![](<../.gitbook/assets/capture (2) (2) (2) (2) (2) (1).png>)

And turn browser sandbox off by toggling the the on/off switch

![](<../.gitbook/assets/capture1 (1).png>)

&#x20;

