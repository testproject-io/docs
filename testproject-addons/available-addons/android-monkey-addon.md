# Android Monkey Addon

The Android Monkey addon help testers execute random tests for any Android application. All you need to do is create an empty test and create a single step of Android Monkey. All default values are set for you so don't need to do anything else. If you want your test to generate more steps, simply increase the 'NumEvents' parameter. For adding a delay between the steps, increase the 'Throttle' parameter.

This addon will execute random tests on your app, stress your application and help you to find hidden bugs. Ideal use of this addon is post-build, pre-production release, after sanity run, after regression run. To make it more advanced, you can control the type of events by providing percentages in the 'pct\*' parameters.

This addon is a wrapper for the Android Monkey program, which you can find more details about here: [https://developer.android.com/studio/test/monkey](https://developer.android.com/studio/test/monkey). It generates pseudo-random streams of user events such as clicks, touches, or gestures, as well as a number of system-level events. You can find more detailed documentation in [the github repo for this addon](https://github.com/testproject-io/addons/tree/master/android-monkey).

