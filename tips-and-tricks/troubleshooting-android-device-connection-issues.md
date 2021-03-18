# Troubleshooting Android Device Connection Issues

If you ever encountered any issues with connecting your android device to your TestProject account, go ahead follow the tutorial below.

{% hint style="info" %}
Supported Android device versions: Android: **5.0** _\(Lollipop\)_ - **11.0**
{% endhint %}

## **Enable "Developer options"**

This could be done by going to: "Settings" -&gt; "About Phone" -&gt; repeatedly tapping the "Build number".

You should get a message that says you've enabled the developer options.

**Inside "Developer options", enable the following:**

* "Stay Awake"
* "USB debugging"
* "Disable Permissions Monitoring" option if it's available
* Under "Select USB configuration" select "MTP" or "File transfer"
* Scroll down and turn the animation off for: "Window animation scale", "Transition animation scale", "Animator duration scale".
* When you plug the USB cable to your Android device, you will be asked 2 things:

  * Allow access to device data -&gt; select "YES"
  * Allow USB debugging -&gt; select "OK"

{% hint style="info" %}
`In case your mirroring/recording still does not work, go to the developer options, clear trusted computers, unplug and replug.`
{% endhint %}

## **Xiaomi/Oppo extra permissions**

In Xiaomi/Oppo devices, there is an extra layer of security that you need to enable in the developer option in order to connect your device and work with TestProject.

* Enable the "USB debugging \(security option\)" option. To do this, you will need to have a SIM card in your device.
* Enable the "Install via USB" option**.**
* Try going to the device settings and Disabling Permission Monitoring.
* If none of the above helped you, try to disable the "MIUI Optimization" option

## **Xiaomi battery settings**

When automating tests on Xiaomi devices, the device's background power consumption setting may be interfering with our automation app.

You will need to disable this setting, by disabling Xiaomi's UIAutomator battery usage control. You can do this by heading to your device's settings:

![](../.gitbook/assets/1%20%283%29.png)

Then go to "Battery & performance":

![](../.gitbook/assets/2%20%283%29.png)

Select "Manage apps battery usage":

![](../.gitbook/assets/3%20%284%29.png)

Select "Choose apps" from the "Manage apps battery usage":

![](../.gitbook/assets/4%20%284%29.png)

Select Installed apps and choose UIAutomator, and then tap on "No restrictions":

![](../.gitbook/assets/5%20%284%29.png)

## **Huawei extra permissions**

If you cannot mirror and view your Huawei Android device, make sure to enable the following settings in your device's developer options:

* Enable "Allow ADB debugging in charge only mode":

![](../.gitbook/assets/6.jpg)

*  Tap on Select debug app and choose either Chrome or uiautomator server.

