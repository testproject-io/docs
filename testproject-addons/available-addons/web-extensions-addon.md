# Web Extensions Addon

TestProject come with many powerful built-in actions. The web extensions addon expands on these and gives you access to many actions that are helpful in creating good tests. These actions are all applicable for web tests only and not for mobile tests.

`Accept alert` - Accepts an alert by clicking on the 'OK' button of the alert

`Add Cookie` - Adds a cookie to the page. This action has the following inputs:

* Name - The name for the cookie
* Value - The value the cookie should have
* Domain - The domain the cookie is visible to
* Path - The path the cookie is visible to
* Expiry - The cookies expiry date
* Secure - Default value is false. Set to true if the cookie requires a secure connection
* HttpOnly - sets whether or not the cookie is an Http only cookie. Set it to true or false

`Clear local storage` - Clears the local storage

`Click and hold` - Clicks and holds the mouse button at the last known mouse coordinates

`Context click` - Right-clicks the mouse at the last known mouse coordinates

`Delete a cookie` - Delete the given cookie from the current domain. This action requires you to specify the name of the cookie to delete

`Delete all cookies` - Delete all the cookies for the current domain.

`Deselect all options` - Clear all selected entries on the given element

`Deselect all options by value attribute` - Deselect all options on the given element that have a specified value attribute. This action requires you to specify the value attribute that you want to match against

`Deselect an option by index` - Deselect an option on the current element by it's given index. Note that the index starts from 0. This action requires you to specify the index of the option you want to deselect

`Dismiss alert` - Dismisses an alert by clicking on the 'Cancel' button of the alert

`Double click` - Double-clicks the mouse at the last known mouse coordinates

`Execute JavaScript` - Executes the specified JavaScript code. This actions requires you to input the JavaScript code that you want to execute. You can also optionally specify the script arguments for your code if it is written as a method

`Get alert text` - Return to a parameter the text in the alert. To effectively use this action you will need to specify a parameter for the alert text to be saved in.

`Get attribute value` - Retrieves the value of an attribute on the given element. The action requires you to fill out the AttributeName field with the name of the attribute you want the value for.

`Get cookie` - Return a specific cookie by name. This action requires you to specify the name of the cookie you want to get

`Get CSS value` - Get CSS value from the given element. This action requires you to specify the name of the CSS property you are interested in, in the Property name field

`Get current window handle` - Return an opaque handle to the current window that uniquely identifies it within the current driver instance

`Get item from local storage` - Retrieves an item from local storage This actions requires you to specify the name of the item you want to retrieve in the Key field. Local storage items can be created with the `Set value for item in local storage`action

`Get windows handles` - Return a set of window handles for all currently open windows

`Maximize window` - Maximizes the current window

`Move mouse by offset` - Moves the mouse from current position by the given offset. This action requires two inputs. The XOffset specifies the number of pixels to move along the x-axis and the YOffset specifies the number of pixels to move along the y-axis

`Move mouse to element with offset` - Moves the mouse to an offset from the top-left corner of the given element. This action requires the specification of two inputs. The XOffset specifies the number of pixels to the right of the top left corner \(negative values will move the offset to the left\) and the YOffset specifies the number of pixels down from the top left corner with negative values moving the offset up.

`Press and hold key` - Performs a modifier key press \(kept pressed\). This action requires an input called TheKey which specifies the key to be kept pressed as a Unicode PUA \(Private Use Area\) code point. Use the `Release pressed key` action to release the key

`Release left mouse button` - Releases the mouse button at the last known mouse coordinates

`Release pressed key` - Releases the key \(shift, ctrl, etc\) that was pressed by the `Press and hold key` action. This action requires an input called TheKey which specifies the key to be released as a Unicode PUA \(Private Use Area\) code point.

`Remove item from local storage` - Removes an item from local storage.This actions requires you to specify the name of the item you want to remove in the Key field.  Local storage items can be created with the `Set value for item in local storage`action

`Select all options by value attribute` - Select all options with selected value attribute. This action requires you to specify the value attribute that you want to match against

`Select allows multiple selection?` - Checks whether the current element supports selecting multiple options at the same time

`Select an option by index` - Select an option on the current element by it's given index. Note that the index starts from 0. This action requires you to specify the index of the option you want to select

`Select options by text` - Select any options on the current element that have text matching the value parameter you specify

`Send keys to alert` - Sends keys \(text\) to an alert. This action requires you to specify the text to write into the alert box in the Keys input field

`Set attribute value` - Sets the value of an attribute on the given element. This action requires you to specify the AttributeName and the AttributeValue fields with the name of the attribute you want to modify and the value you want to assign to it.

`Set value for item in local storage` - Set \(or create\) the value for item in local storage. This action requires you to specify the Key for local item and the Value that you want to set it to.

`Set window position` - Set the position of the current window relative to the upper left corner of the screen. This action requires the X and Y inputs to specify the number of pixels to move right and down from the top left corner. 

`Set window size` - Set the size of the current window. This action requires Width and Height inputs to specify how big the window should be

`Wait for alert presence` - Wait until the alert is displayed. This action requires you to specify the timeout for how long to wait until and alert is present \(default timeout is 0\)

