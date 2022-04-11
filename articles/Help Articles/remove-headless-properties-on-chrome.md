---
description: >-
  This article describes how to minimize the difference between chrome headless
  and normal chrome browser at execution
---

# Remove Headless properties on Chrome

Sometimes when we execute a test in chrome headless it behaves differently than in our normal browser, this article will help you minimize the effect of using a headless browser and help you reduce flakiness when executing on headless.

Chrome Headless browser has different properties, for example:

#### User-Agent <a href="#h_f819618cff" id="h_f819618cff"></a>

Chrome uses — `Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_6) AppleWebKit/537.36 (KHTML, like Gecko)`` `**`Chrome`**`/63.0.3205.0 Safari/537.36`

Chrome Headless — `Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_6) AppleWebKit/537.36 (KHTML, like Gecko)`` `**`HeadlessChrome`**`/63.0.3205.0 Safari/537.36`

#### **Accept-Language:** <a href="#h_1463156701" id="h_1463156701"></a>

There is also a difference in the request header Accept-Language:

Chrome uses — `en-US,en;q=0.8`

Chrome Headless doesn’t set this header.

#### Resolution: <a href="#h_c5b1710fd4" id="h_c5b1710fd4"></a>

Make sure you are using the same resolution on Chrome Headless and normal chrome browser for your executions.

#### Solution: <a href="#h_9d1b23ac39" id="h_9d1b23ac39"></a>

We can change these properties using the Selenium Desired Capabilities to start the driver with properties similar to normal Chrome:

```json
{
   "goog:chromeOptions":{
      "args":[
         "--user-agent=Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/94.0.4606.61 Safari/537.36",
         "--lang=en",
         "--start-maximized"
      ],
      "excludeSwitches":[
         "enable-automation"
      ]
   }
}
```

You can set them on TestProject on the job like this:

![](<../../.gitbook/assets/image (2) (2) (1).png>)

* Be sure to **remove headless** from the User-Agent, use [this site ](https://developers.whatismybrowser.com/useragents/explore/software\_name/chrome/)to determine your user agent.
* Request your application in the correct language in "lang=en"
* Use excludeSwitches to remove the "Chrome is being controlled by automated test software" if needed.
* Set resolution ("--window-size=1920,1080") or start maximized to set the same resolution you use on normal Chrome
