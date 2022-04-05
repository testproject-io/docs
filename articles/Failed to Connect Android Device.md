# Failed to Connect Android Device

The TestProject Agent identifies all the Android devices/emulators that are running and connected to your machine.\
If your are experiencing some issues with your Android device, such as the following: Can't record a test, can't get the device mirroring or access to the application list in the device - Please try this troubleshooting article.

1. **Did you enable all the relevant settings in the developer options?**\
   a. Enable developer options: **"Settings" -> "About Phone" -> repeatedly tapping the "Build number"**. You should get a message that says you enabled developer options.\
   \
   b. Inside the developer options, enable: **"Stay Awake", "USB debugging", Under "Select USB configuration" select "MTP".**\
   Then, scroll down and turn the animations off for: **"Window animation scale", "Transition animation scale", "Animator duration scale".**\
   When plugging in the USB cable to the Android device, you will be asked 3 things: **Allow access to device data -> select "YES", Allow USB debugging -> select "OK"**\

2. **API level is supported by the agent?**\
   Make sure that your Android OS version (API Level) is greater or equals to the minimum OS Version that the Agent supports. You can verify it by checking here: **C:\Program Files\TestProject Agent\minicap\libs** (make sure you can find the folder for that version). The minimum version we support is Android 5.0 which is OS version 21.\

3. **Check if the ADB can detect the device**\
   \
   **Windows:**\
   Open the Agent's installation folder: **C:\Program Files\TestProject Agent\android-sdk\platform-tools** and check if there is an ADB executable (adb.exe file).\
   \
   **OS X:**\
   Open the Agent's installation folder: **"/Applications/TestProject Agent.app/Contents/Resources/android-sdk/platform-tools”** and check if there is an ADB executable (adb file).\
   \
   If the adb file **exists**, open the terminal/command-prompt from within this folder and run this command: (Windows) **adb devices** (OS X) **./adb devices**\
   You should see a list of all the connected devices. If you don't see any device in the list, try to change the USB port/cable. Also, check if the USB Configuration is set to MTP/File transferring.\
   \
   If the adb.exe file **does not** exist, maybe you unchecked the ADB option while installing the Agent. Try to re-install the Agent and check the ADB option.\

4. **Is the device listed in the Agent's devices list?**\
   If the device is listed in the devices list in your Agent tab, but there is an issue recognizing device in recorder, check if the **UIAutomator2** application is installed on the device. Search the application in: **"Settings" → "Apps" → search for uiautomator2**. If you **found these two apps**:\
   \
   _io.appium.uiautomator2.server_\
   _io.appium.uiautomator2.server.test_\
   \
   delete them and then try to connect the device again (The Agent will install these apps automatically).\
   \
   If you **don't have these apps**, then there's a problem with the installation. You can try the following:\
   Navigate to the installation folder: (Windows) **"C:\Program Files\TestProject Agent\android-sdk\platform-tools"** (OS X) **"/Applications/TestProject Agent.app/Contents/Resources/android-sdk/platform-tools”**\
   and then open the terminal/command prompt from that location.\
   Type these commands in the command prompt:\
   **Windows:**\
   \* _adb install "C:\Program Files\TestProject Agent\appium\apk\android-driver.apk"_\
   \* _adb install "C:\Program Files\TestProject Agent\appium\apk\android-driver-test.apk"_\
   **OS X:**\
   _\* ./adb install "/Applications/TestProject Agent.app/Contents/Resources/appium/apk/android-driver.apk”_\
   \* _./adb install "/Applications/TestProject Agent.app/Contents/Resources/appium/apk/android-driver-test.apk”_\
   This should install the two UIAutomator applications that the Agent failed to install. If it still doesn't work, proceed to the next step.
5. Try going to the device settings and **Disabling Permission Monitoring.**
6. **If none of the above steps helped, then factory reset of the device should solve the issue.**
