---
description: >-
  Firefox profile, Firefox, Permission, Pop-ups, desired capabilities,
  Extensions and auto download files
---

# Using Firefox Profile with Selenium Desired capabilities - Permissions & Extensions

### Why should we use a Firefox profile? <a href="#h_1de6e4a65f" id="h_1de6e4a65f"></a>

#### 1) Manage Permissions: <a href="#h_f780ad370a" id="h_f780ad370a"></a>

If your website prompts you with a lot of pop-ups about permissions or access, or to choose what to do with saved files we can overcome it using a firefox profile.

**2) Using browser extension**

Using Firefox profile allows you to start your execution and extensions pre installed.

#### How to do this with TestProject? **(first, we need agent version 3.2.0 and above)** <a href="#h_8849e244dc" id="h_8849e244dc"></a>

To use Selenium Desired capabilities we first need to create a job. then we should assign all the tests we need a firefox profile into this job.

**Where can we find the Firefox profile?**

Firefox keeps the profile locally in a different location in each system.

you can see the path to the profile folder by opening Firefox browser, and search in the URL search bar the address:

```
about:profiles
```

![](<../../.gitbook/assets/image (463).png>)

### What is the Best Practice? <a href="#h_d9397b918a" id="h_d9397b918a"></a>

What we should do, is to create a designated profile for us to use in our jobs.

1\) We can do it by adding a firefox profile like this:

Open Firefox browser, and search in the URL search bar the

address:

```
about:profiles
```

then click on Create a New Profile

![](<../../.gitbook/assets/image (549).png>)

2\) After we have created the firefox profile we need to open firefox with this profile and add our application URL to the permissions we need.

(use about:profiles to check current profile)

![](<../../.gitbook/assets/image (460).png>)

3\) We can set the following Selenium Desired capabilities on our job:

![](<../../.gitbook/assets/image (484).png>)

And add these capabilities:

```json
{
  "moz:firefoxOptions": {
    "profile_path": "C:/Users/{userName}/AppData/Roaming/Mozilla/Firefox/Profiles/{profile}"
  }
}
```

_\*Don't forget to replace {userName} and {profile} with your directory\*_

### Using Firefox Profile to Auto download files (GUI / Headless) <a href="#h_bf244e632d" id="h_bf244e632d"></a>

If you want to automatically download files and avoid the download window pop-up you will need to add your type file to Firefox applications settings and change it to save files.

To change these settings follow these steps:

1\) Navigate to your application and download the file that will be used in the test. Open it with a default app and tick the check box **(do this automatically for files like this from now on)**

For **example** zip file (open with WinRar):

![](<../../.gitbook/assets/image (546).png>)

2\) Click on the zip file option in Firefox settings under the Applications section and change it from always ask to save the file, this will automatically save the file to the default directory.

![](<../../.gitbook/assets/image (543).png>)

\*Note - Firefox ability to automatically save the content type may vary dependent on the file type\*

#### Use already made base64 profile that contains the following MIME types: <a href="#h_bcd14182fa" id="h_bcd14182fa"></a>

```
application/msword
application/ms-doc
application/doc
application/pdf
text/plain
application/text
text/xml
application/xml
text/csv
application/xlsx
application/yaml
application/json
application/java-archive
image/jpeg
application/zip
application/octet-stream
```

Firefox base64 Job capabilities:

```json
{
  "moz:firefoxOptions": {
    "profile": "UEsDBBQACAgIADBzZ1MAAAAAAAAAAAAAAAAHAAAAdXNlci5qc52XS2/jNhCA7/0VhU8tUDPJpnvZnNJsFlggaIrNBnsUKGok0aZIlkNadn99h5IVW5YsOXsTyeFjZr55KCC4xDrIf1ukztQ0YshzaL6lLljFVc0dMNA8VZAt/vg15wrh97tfwmFnxj3JWON83FICV75sx4yENlLM7O9uzkytleEZ20ioo/xX7cFprtSuO+D7zgLSKYvF+BElKAvu3lpkGjb0hWtSaAPfzWeJ67iRW6uk4F4afVVhbVx2159aZkb0pk7HNsvvPGz9lVVc6t5SnG7XtpXqrcRxsyBw019QuO1N7PjJ1hWa/i0rvuFL7kQpN3AnK17A1cpC0ZP5T9re2AgPfoneAa9ObKfBkxnWrPTeMltKLHfLuGw54lKBLnxJhvvw8eO4yenELDoPPNAd2Rfp0N8TCkIBbfMunNJiKsJqm4jSmQoSFE5an7igEy+ruOX2evwiz1NkRKN+1g/KIFwIU8U1WYi4Lk39owT9QrBGUMe3W3qU9RgvSyqTcTWDPmy8MQoZOGecMBqNOqZ9qD7KQhtNVqugSsG9NEOc1gUBkZyI3lAoOsBAdsvpoYlwHMvpvUrqNTMWdEL0NdEUnfnuAM6jW78FPX5ZDWnmiEaXcCGA3Bk0aY6EQyLAeRy1xJunJFIk7SB7vLl++dsQOdG1f44L01T2rH9ITf7Fm2sm6SLz+u2pCe3UBP8pVVyvF0PmWoUSyibJCskY8Z2yNf3wbVsrydwky+pSelASPR3wb5DuHAkRg7X0bB9NHXWkXGRh0gCKk2MoAKZRw8htsKykqLF0dlKDEjGCglMTGfEtDnKjKE6fSJMhABEN3SDGgiUagGnyQ757JZF35/xg432Pk7qACE76HWGlgL4YJSYpfGKcLKROrKG8tZvmWkNNMcr2yk+4vvfQ9mQWJ19CWskmrv5pJu8bci+rcaPHTGr8Fsp7L0YPkuSZVHcIWlKzbmAfOs3kOcnBksdqR6iaOkl3SQY5D8qP557O7ALtHrbx1w55mESzY58ChdKadzvWptFG/sOc7EW9wePr0z27ZfzgpKF6sS625WQyA5+6oguoaY66Kik4pY0NLCMKXC0vanCGOjtYNdVy8oEt4vFp08cfeYsHHzudKPwiTNsr3czX02dCbfbsVBmxbjLhRR5DiC3Knp+5Wl2xlnKWhcpOeo9ov4jJHjiGSpOT2XgaHiSj0yx0O05Cm+KXXRgSTj7MFPK97JkUs2+M5juio3KLTTNwKLeUikKTsyctFzEZf8RRDJm2PjaN01f90PY2Z1u6faFLmqyVkRl1kcQ6cKbNyvIVdntmwpR6esVECWL9uc1tf7Ur7y+TjGeZjErxmaIx+i/0s/9AyhRFnNx3h5Nl4ijcGo0fKI1SA59KFQHVsii9mimMAwN08LOKGsgGvkVsOh2cKH3oeWKPSjBTpznT9BxiXeUYbFv+D+3I/1BLBwhquWbIOwQAAF4OAABQSwECFAAUAAgICAAwc2dTarlmyDsEAABeDgAABwAAAAAAAAAAAAAAAAAAAAAAdXNlci5qc1BLBQYAAAAAAQABADUAAABwBAAAAAA="
  }
}
```

### Use Firefox Profile with the open SDK (Java code) <a href="#h_7cb6118385" id="h_7cb6118385"></a>

**You can pass the profile in several ways:**

1\. You can create a fresh profile and set preferences for it, and then set that profile in the options.

Here is an example of how to set preferences to download files automatically in Firefox without presenting the dialogue:

```java
FirefoxOptions options = new FirefoxOptions();
        FirefoxProfile profile = new FirefoxProfile();
        profile.setPreference("browser.download.folderList", 2);
        profile.setPreference("browser.download.dir", "C:\\Temp");
        profile.setPreference("browser.download.useDownloadDir", true);
        profile.setPreference("browser.download.viewableInternally.enabledTypes", "");
        profile.setPreference("browser.helperApps.neverAsk.saveToDisk", "application/msword;application/ms-doc;application/doc;application/pdf;text/plain;application/text;text/xml;application/xml");
        options.setProfile(profile);
        FirefoxDriver driver = new FirefoxDriver("{TP_DEV_TOKEN}", options);
```

2\. You can also create a profile out of a local path on your system:

```java
FirefoxOptions options = new FirefoxOptions();
FirefoxProfile profile = new FirefoxProfile(new File              ("C:/Users/Username/AppData/Roaming/Mozilla/Firefox/Profiles/MyProfile.test"));
    options.setProfile(profile);
    FirefoxDriver driver = new FirefoxDriver("{TP_DEV_TOKEN}", options);
```
