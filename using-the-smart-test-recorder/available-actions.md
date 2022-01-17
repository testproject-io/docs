# Available Actions

Actions are a way to 'do something' within TestProject. There are a few different types of actions. Some actions act on an element while others do not. There are many actions directly built into TestProject which are outlined below. Many additional actions can also be found through the various available [addons](../testproject-addons/what-is-an-addon.md).

The table below shows the various system level actions that are part of the core TestProject tool. The `Action Type` column shows if the action acts on an element or not. The `Action Name` column gives the name of the actions which can be used to search for that action and the `Action Description` column gives a short explanation of what that action does.

| Action Type | Action Name | Action Description |
| :--- | :--- | :--- |
| Element | Clear contents | Clears element contents \(deletes any existing text\) |
| Element | Click | Clicks an Element |
| Element | Click if visible | Clicks on an element only if it is visible |
| NonElement | Close App | Closes AUT \(App Under Test\) |
| Element | Contains text? | Checks if an element contains the given text |
| NonElement | Get current URL | Retrieves the current URL |
| Element | Get text | Retrieves a text from an element |
| NonElement | Get title | Retrieves a title of a browser or an application |
| Element | Is clickable? | Check if element is clickable |
| Element | Is invisible? | Checks if an element is invisible or not present on the Screen/DOM |
| Element | Is present? | Checks if an element is present on the Screen/DOM |
| Element | Is selected? | Checks if an element is selected |
| Element | Is visible? | Check if element is visible \(and has width/height &gt; 0\) |
| NonElement | Launch app | Launch the app which was provided in the capabilities at session creation |
| Element | Long press gesture | Makes a long press gesture |
| Element | Move mouse to element | Moves the mouse to the middle of the element and element is scrolled into view |
| NonElement | Navigate back | Back browser navigation |
| NonElement | Navigate forward | Forward browser navigation |
| NonElement | Navigate to URL | Browser navigation to the specified URL |
| NonElement | Pause | Pauses the execution for the defined time \(in milliseconds\) |
| NonElement | Refresh | Refreshes the current browser tab |
| NonElement | Reset App | Reset AUT \(App Under Test\) |
| NonElement | Scroll window | Scrolls the document by the specified number of pixels |
| Element | Select an option by value | Select an option that has a value matching the argument |
| NonElement | Send key event | Send a key event to the device |
| NonElement | Send Keys | Sends Keys \(e.g. TAB\), see https://goo.gl/jg18sk for full list |
| NonElement | Set iFrame size in Recorder | Sets iFrame size in Recorder |
| NonElement | Start Activity | Launches an Android Activity |
| NonElement | Swipe gesture | Makes a Swipe gesture |
| Element | Tap | Taps element |
| NonElement | Tap gesture at coordinates | Makes a Tap gesture at specified coordinates |

