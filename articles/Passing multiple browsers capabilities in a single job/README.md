---
description: >-
  Capabilities, jobs, Chrome/Firefox/Safari/Edge/IE, multiple desired
  capabilities
---

# Passing multiple browsers capabilities in a single job

To learn more on desired capabilities please visit previous articles [here](https://intercom.help/testprojectio/en/?q=capabilities).

To pass multiple capabilities in a single job we need to use a custom structure.

That structure has to be a valid JSON object without duplicate keys.

For example here is a structure for capabilities for Chrome in a job:

```json
{
"browserName": "chrome",
  "goog:chromeOptions": {
    "args": [
      "--window-size=1080,1080"
    ]
  }
}
```

In order to achieve capabilities for multiple browsers we need to omit the "browserName", we can then use the following structure:

```json
{
  "ms:edgeOptions": {
    "args": [
      "--inprivate"
    ]
  },
  "goog:chromeOptions": {
    "args": [
      "--incognito"
    ]
  },
  "moz:firefoxOptions": {
    "args": [
      "-private"
    ]
  },
  "se:ieOptions": {
    "args": []
  },
  "safari.options": {
    "args": [
      "--use-fake-ui-for-media-stream"
    ]
  }
}
```

Note:

1\) Any browser you select in the job will be affected by the capabilities provided under the "options" key.

2\) If you do not select all the browsers you provided capabilities for it should only affect the ones selected.

3\) Under "args" array the same arguments can be set across browsers, however note that they **may vary between browsers.**
