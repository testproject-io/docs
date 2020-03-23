# Deep Link Toolkit Addon

This addon will open deep links reliably across Android and iOS platforms using the strategy outlined in [Appium Pro Edition 84](https://appiumpro.com/editions/84). Deep links can cut out huge amounts of time from your test, if you have them built into your app!

**Available Action**

`Open Deep Link` - Opens a deep link

This action requires the following input parameters:

* `URL` - The deep link url you want to open
* `Pkg` - \(optional\) The package of the app for the URL if you want to open a different app than the one that is currently running. If left blank this will default to the currently running app. 

