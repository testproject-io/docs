# JSON Operations Addon

This addon has actions to validate, search and get values from a JSON string object. It uses JsonPath which is a Java DSL for reading JSON documents. You can find documentation on how to use JsonPath queries [here](https://github.com/json-path/JsonPath)

### Available Actions

`Does a property exists in a JSON object?` - Checks if a certain property exists in a JSON object

This action takes in the following inputs:

* `JsonFile` - The JSON string you want to check for the existence of the property in
* `JsonPath` - The JayWay JsonPath value to search for in the `JsonFile` 
* `ExpectedResult` - Whether you expect to find the `JsonPath` in the `JsonFile` \(true\) or not \(false\)

`Get value from JSON using JsonPath` - Provides search ability in JSON objects using JsonPath.

This action takes in the following inputs:

* `JsonFile` - The JSON string you want to check for the value in
* `JsonPath` - The JayWay JsonPath value to search for in the `JsonFile` 

`Is valid JSON?` - Checks if the given string is a valid JSON object

This action takes in the following inputs:

* `JsonString` - The JSON string you want to check the validity of
* `ExpectedResult` -  If you expect the string to be valid or not \(true/false\)

`Is valid JSONArray?` - Checks if a given string represents a JSONArray object

This action takes in the following inputs:

* `JsonString` - The JSON string you want to check the validity of
* `ExpectedResult` -  If you expect the string to be a valid json array object or not \(true/false\)

`Is valid JSONObject?` - Checks if a given string represents a JSONObject

This action takes in the following inputs:

* `JsonString` - The JSON string you want to check the validity of
* `ExpectedResult` -  If you expect the string to be a valid json object or not \(true/false\)

`Extract multiple JsonPaths` - **Extract up to 10** JsonPath values in one action.

This action takes in the following inputs:

* `JsonFile`- The JSON object to extract values from.
* `JsonPaths`- The JsonPaths values to search for, **delimited by a new line**.

