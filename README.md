# Troubleshooting DevToolsActivePort file doesn't exists

The recorder is crashing with the error Operation failed please try again.

In the agent logs you can see the error message

Caused by: org.openqa.selenium.WebDriverException: unknown error: Chrome failed to start: crashed. \(unknown error: DevToolsActivePort file doesn't exist\).

This can happen in several scenarios:

1. TestProjects support Chrome versions 77 and newer, make sure the Chrome version installed on your machine \(including other users\) is suitable. You can find the Chrome version by navigating to`chrome://version/` in the browser and looking at the first line ![](.gitbook/assets/image%20%28224%29.png) 

   To update Chrome go to the 3 dots next to the profile icon on the top toolbar &gt; help &gt; About Google 

   Chrome

    ![](.gitbook/assets/image-1-.png) 

2. The Agent is running as administrator. Running and installing the Agent should be as regular user, not as administrator.
3.  If the above options didn't solve the issue go to `C:\Users\<username>\AppData\Roaming\TestProject\Agent` and add a file called `debug-configuration.json` with the content

   `{ "tp.config.chrome.no.sandbox" : "true" }`

4. In case you are using Quick Heal antivirus you need to disable browser sandbox.
   1. Open Quick Heal Total Security dashboard
   2. Go to Protection and select Browser Sandbox

      ![](.gitbook/assets/capture%20%281%29.png) 

   3. Turn browser sandbox off by toggling the the on/off switch ![](.gitbook/assets/capture1.png) 

 

