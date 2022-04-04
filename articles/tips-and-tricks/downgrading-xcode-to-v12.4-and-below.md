---
description: How to downgrade Xcode to version 12.4 and below.
---

# Downgrading Xcode to v12.4 and Below

If you've noticed you cannot record or execute tests on simulators on your Mac, the issue may be caused by the version of Xcode you're using.

If you're using Xcode version 12.5 or above, you'll need to downgrade your Xcode version to 12.4 or below and set it as the active Xcode of your system.

To start you'll need to either:

1. Remove the currently installed Xcode from your system.
2. Rename the Xcode.app in your finder to something else, like Xcode-12.5.app.

Then you'll need to head into the [official Apple site](https://developer.apple.com/download/more/?=xcode), and download then install your choice of Xcode:

![Apple Download Center.](<../../.gitbook/assets/image (426).png>)

After downloading an installing this version of Xcode, you'll need to set it as the active one on your system.

To do so, you can run the following command in your terminal:

```
sudo xcode-select --switch path/to/Xcode.app
```

You can find more details on how to set your active Xcode developer directory in the help article located [here](https://intercom.help/testprojectio/en/articles/4826614-using-ios-simulators-with-testproject).

{% hint style="info" %}
Note, you will need to set the path to the correct path of the newly installed Xcode.
{% endhint %}

