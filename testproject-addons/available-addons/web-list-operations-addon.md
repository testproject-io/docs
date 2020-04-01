# Web List Operations Addon

This addon provides actions to count items and retrieve their values for drop-downs and ordered/unordered lists on a web page. The actions in this addon are only available for web tests and not for mobile tests. It is also only available on list or select elements.

### Available Actions

`Check if all items in a web list element contain text` - Checks if all items inside an HTML web list element contain specific text.

This action takes in the following input parameters

* `Text` - Text to check for in each item of the list
* `ExpectedResult` - Expected result. Specify true if you expect each item to contain the given text and false if you do not

`Click on the Nth item in a web element` - Clicks on the Nth item inside a web list element. To use this action you will need to specify the index of the item you want to click on in the `Index` input parameter field

`Count items in a web list element` - Counts the elements inside an HTML web list element

`Get text from the Nth child in a web list element` - Returns the text of the Nth element inside a web list element. To use this action you will need to specify the index of the item you want to click on in the `Index` input parameter field

 

