---
description: Autologin, Chrome Profile, permission pop-ups, desired capabilities.
---

# Using Chrome Profile with Selenium Desired capabilities - Autologin & Permissions

#### **Why should we use a Chrome profile?** <a href="#h_f4fba39ec3" id="h_f4fba39ec3"></a>

**1) Autologin:**

Selenium opens the browser in incognito mode. However, for some test scenarios, we would like to log in to a Google account. Instead of doing it as part of the test flow or we can do it automatically.

**2) Manage Permissions:**

If your website prompts you with a lot of pop-ups about permissions or access, we can overcome it using a chrome profile.

#### **How to do this with TestProject?** <a href="#h_aa7c6e8dfe" id="h_aa7c6e8dfe"></a>

To use Selenium Desired capabilities we first need to create a **job**. then we should assign all the tests we need a chrome profile into this job.

Where can we find the default profile?

Chrome keeps the default profile locally in a different location in each system.

In Windows:

```
C:\Users\{username}\AppData\Local\Google\Chrome\User Data\default
```

In Mac:

```
/Users/{username}/Library/Application\ support/Google/Chrome/default
```

In Linux:

```
/home/{username}/. config/google-chrome/default
```

However, **using the default profile is not recommended** as it can create a **conflict** between selenium and the regular chrome browser on your machine as both of them try to access the same profile.

#### What is the Best Practice? <a href="#h_d644fc0246" id="h_d644fc0246"></a>

What we should do, is to create a designated profile for us to use in our jobs.

1\) We can do it by adding a chrome profile like this:

![](<../../.gitbook/assets/image (544).png>)

2\) After we created that profile and logged in we should change our site settings to allow all the permissions we need:

![](<../../.gitbook/assets/image (476).png>)

3\) Then we should navigate to:

C:\Users{username}\AppData\Local\Google\Chrome\User Data\\

And make sure we can find the profile we have just created.

![](<../../.gitbook/assets/image (490).png>)

4\) Now let's copy **the entire User Data folder** to our desktop for example.

Why are we creating this new folder?

If any instance of Chrome browser is open while we are trying to create a new WebDriver instance the operation will fail with an error due to conflict of our chrome browser and ChromeWebDriver trying to access the same profile.

To avoid this error or closing the browser every time we run a test we need to create this copy.

**If you see this message please make sure you followed step #4**

_`InvalidArgumentException: Message: invalid argument: user data directory`_

_`is already in use, please specify a unique value for --user-data-dir`_

_`argument, or don't use --user-data-dir`_

5\) Now when we have a folder with all of our data and profiles we can set the following Selenium Desired capabilities on our job:

Use this button:

![](<../../.gitbook/assets/image (507).png>)

And add these capabilities:

```json
{
  "goog:chromeOptions": {
    "args": [
      "user-data-dir=C:/Users/{username}/Desktop/User Data",
      "profile-directory=Profile 2"
    ]
  }
}
```

a) The first arg states the local path to our User Data folder that we created.

b) The second arg allows us to choose the profile that we want to use. (profile to open the browser with)

If you are using Mac or Linux you can do the same the only difference is in the path.

\*Note\*

If you are using Mac the JSON Object does not accept a backslash ‘\’ after the Application it is only required for navigation purposes.

If you are using the SDK just add options (Java code)

```
ChromeOptions options = new ChromeOptions();
options.addArguments("--user-data-dir=PATH_TO/Test User Data");
```

\
