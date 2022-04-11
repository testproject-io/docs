---
description: Here we'll show the proper way to install the mentioned above.
---

# Installing Google-chrome and Chromedriver on an Amazon Linux machine

If you're getting errors while trying to run tests on your Amazon Linux Machine, such as :

"Failed to execute test 'TEST\_NAME' on Chrome: unknown error: Chrome failed to start: exited abnormally."

They are most likely caused by incorrect installations.\
Consider using this helpful guide to install everything you need properly.

**Installing Chromedriver:**

1\. Go to your temp folder:

```
cd /tmp/
```

2\.  Download the latest Linux-based Chromedriver:

```
wget
https://chromedriver.storage.googleapis.com/2.37/chromedriver_linux64.zip
```

3\.  Extract Chromedriver from its archive:

```
unzip chromedriver_linux64.zip
```



4\. Move Chromedriver to the applications folder:

```
sudo mv chromedriver /usr/bin/chromedriver
```

5\. Confirm Chromedriver version:

```
chromedriver --version
```

\
**Installing Google-chrome:**

1\. Use this command to install the newest version of the chrome browser:

```
curl https://intoli.com/install-google-chrome.sh | bash
```

2\. Rename google-chrome-stable with google-chrome, so that automation tests will be able to identify the Chrome browser before test execution starts:

```
mv /usr/bin/google-chrome-stable /usr/bin/google-chrome
```

3\. Verify Chrome installation:

```
google-chrome --version && which google-chrome
```

\
**Manual Google-chrome installation (This is optional)**

1\. Check your Chrome version if already installed:

```
google-chrome --version
```

2\. Get the location of the application library:

```
which google-chrome
```

3\. Remove the older version of Chrome if you don't need it:

```
sudo yum -y erase google-chrome
```

4\. Upgrade to the newest version of Chrome using:

```
sudo yum update google-chrome-stable
```

5\. If you are indeed using Amazon Linux, you'll need to download the rpm file, extract it and move it to /usr/bin:

```
wget https://dl.google.com/linux/direct/google-chrome-stable_current_x86_64.rpm
```
