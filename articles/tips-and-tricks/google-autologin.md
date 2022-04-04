# Google Autologin

**Motivation**

Selenium opens the browser in incognito mode. However, for some test scenarios, we would like to login to Google account. Instead of doing it as part of the test flow or running it as a setup method we can do it automatically.

**How to do this with TestProject?**

1. Chrome keeps the profile locally in

_C:\Users\\{username}\AppData\Local\Google\Chrome\User Data._

We need to go to the parent folder (Chrome) and do one of the following options:

* Create a copy of the User Data folder, let’s call it Test User Data.
* Create a new Chrome profile and set the required actions in it, and then

copy this profile (will probably appear as Person 2) to the Test User Data folder instead of the default user (change the name).

Why are we creating this new folder? If any instance of Chrome browser is open while we are trying to create a new WebDriver instance the operation will fail with

an error

`InvalidArgumentException: Message: invalid argument: user data directory`

`is already in use, please specify a unique value for --user-data-dir`

`argument, or don't use --user-data-dir`

So, to avoid closing the browser every time we run a test (which is quite

impossible when we are using TestProject) we use a copy of the profile.

3\. Now we want to use the new profile

* In TestProject platform [create a job](https://docs.testproject.io/schedule-and-run-tests/create-and-schedule-jobs) and add your test to it. Now click on

the Set Driver Desired Capabilities icon

![](<../../.gitbook/assets/image (398).png>)

And add

```
{
  "goog:chromeOptions": {
    "args": [
      "user-data-dir=C:/Users/dorbe/AppData/Local/Google/Chrome/User Data",
      "profile-directory=Profile 2"
    ]
  }
}
```

* If you are using the SDK just add options (Java code)

```
ChromeOptions options = new ChromeOptions();
options.addArguments("--user-data-dir=PATH_TO/Test User Data", "profile-directory=Profile 2");
```

{% hint style="info" %}
`You can see the current profile you are using by navigating to chrome://version inside your Chromr browser.`
{% endhint %}

``
