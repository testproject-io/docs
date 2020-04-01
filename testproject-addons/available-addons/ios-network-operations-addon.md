# iOS Network Operations Addon

This addon provides actions to change and check the network settings of the iOS device \(e.g. toggle the Wi-Fi, bluetooth, etc.\). It opens the control panel on the iOS device and clicks on the desired settings, and you can use it when you want to set the network state before the test execution. You can also check the network state during or after the test execution.

### Available Actions

`Check Airplane Mode state` - Returns the Airplane Mode state and validates that it matches the expected state

This action requires the `ExpectedState` input parameter to be specified as ON or OFF 

`Check Bluetooth state` - Returns the Bluetooth state and validates that it matches the expected state

This action requires the `ExpectedState` input parameter to be specified as ON or OFF 

`Check Cellular Data state` - Returns the Cellular Data state and validates that it matches the expected state

This action requires the `ExpectedState` input parameter to be specified as ON or OFF 

`Check Wi-Fi state` - Returns the Wi-Fi state and validates that it matches the expected state

This action requires the `ExpectedState` input parameter to be specified as ON or OFF 

`Get Airplane Mode state` - Gets the Airplane mode state of the iOS device

`Get Bluetooth state` - Gets the Bluetooth state of the iOS device

`Get Cellular Data state` - Gets the Cellular Data state of the iOS device

`Get Wi-Fi state` - Gets the Wi-Fi state of the iOS device

`Toggle Airplane Mode ON/OFF` - Toggles Airplane Mode ON/OFF

`Toggle Bluetooth ON/OFF` - Toggles Bluetooth ON/OFF

`Toggle Cellular Data ON/OFF` - Toggles Cellular Data ON/OFF

`Toggle Wi-Fi ON/OFF` - Toggles Wi-Fi ON/OFF

