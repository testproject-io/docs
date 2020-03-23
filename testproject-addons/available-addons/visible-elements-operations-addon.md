# Visible Elements Operations Addon

This addon provides actions the will perform only if the element is visible. The actions will not fail the step in case the element is not visible.

### Actions

`Clear contents (if visible)` - Clear the contents of the current element if it's visible

`Click if visible` - Click the current element if it's visible

This action has one input, `Timeout` which specifies how long the action will wait for the element to become visible. The default, if you leave it blank is 3 seconds

`Contains text? (if visible)` - Check if the current element contains the specified text?

This action has the following inputs:

* `Text` - The text you want to verify is in the element
* `Timeout` -  how long the action will wait for the element to become visible. The default, if you leave it blank is 3 seconds

`Get text (if visible)` - Get text from element if it's visible.

This action has one input, `Timeout` which specifies how long the action will wait for the element to become visible. The default, if you leave it blank is 3 seconds

`Is clickable? (if visible)` - Check if the current element is clickable.

This action has one input, `Timeout` which specifies how long the action will wait for the element to become visible. The default, if you leave it blank is 3 seconds

`Long press gesture (if visible)` - Make a long press gesture on the current element if it's visible \(Andoid and iOS only\).

This action has the following inputs:

* `Duration` - The amount of time \(in milliseconds\) to hold the press for
* `Timeout` -  how long the action will wait for the element to become visible. The default, if you leave it blank is 3 seconds

`Tap (if visible)` - Tap the current element if it's visible \(Android and iOS only\)

This action has one input, `Timeout` which specifies how long the action will wait for the element to become visible. The default, if you leave it blank is 3 seconds

`Type text (if visible)` - Type the specified text in the current element if the element is visible

This action has the following inputs:

* `Text` - The text you want typed into the element
* `Timeout` -  how long the action will wait for the element to become visible. The default, if you leave it blank is 3 seconds

