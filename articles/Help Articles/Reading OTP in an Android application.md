---
description: Here we will discuss how to get OTPs when creating a mobile test.
---

# Reading OTP in an Android application

If you want to get an OTP from an SMS message, you will need to download and install the "Android SMS OTP Automation" addon located here:\
[https://addons.testproject.io/android-sms-otp-automation](https://addons.testproject.io/android-sms-otp-automation)\
\
The addons bring you three new actions:\
&#x20;1\. Getting OTP by regex.\
&#x20;2\. Getting OTP by keywords.\
&#x20;3\. Getting OTP by index.\
\
Here's an example of getting an OTP by keywords:\
First, create the step by finding the appropriate action.\


![](https://downloads.intercomcdn.com/i/o/494781513/b1b0ae70368513c8232ff0a4/image.png)

![](https://downloads.intercomcdn.com/i/o/494781644/36284fa27c06367d2e1ea6b1/image.png)

\
After creating the step, you need to set the parameters.\
Here you can set the amount of time to wait for the SMS to be received by the mobile device and the words to exclude from it to get the OTP separated by commas.\
\
Each action has different parameters, and it's up to you to decide which one fits better for your test, so don't be afraid to experiment while.
