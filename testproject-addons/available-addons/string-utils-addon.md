# String Utils Addon

This addon provides string utilities that can be use to manipulate strings in various ways.

### Available Actions

`Compare two strings` - Compares the two given strings lexicographically. Each character of both the strings is converted into a Unicode value for comparison.

This actions takes in the following input parameters:

* `FirstString` - The first string you want to compare
* `SecondString` - The second string you want to compare
* `IgnoreCase` - Set to true to ignore case difference and to to false to consider case differences in the comparison

`Concatenate two strings` - Concatenates the second string to the end of the original string.

This action takes in the following input parameters:

* `FirstString` - Original \(source\) string
* `SecondString` - String to be added to end of `FirstString` 

`Convert string to lowercase` - Converts a given string to lowercase.

This action has the input parameter `InputString` where you put in the string you want to convert to lowercase.

`Convert string to uppercase` - Converts a given string to uppercase.

This action has the input parameter `InputString` where you put in the string you want to convert to uppercase.

`Find last index of substring from index` - Returns the index within the source string of the last occurrence of the specified substring, searching backward starting at the specified index.

This action takes in the following input parameters:

* `SourceString` - Source string to search for occurrences in
* `SubString` - Substring to search for in `SourceString` 
* `FromIndex` - Index to start searching from. \(searching will go backwards from this index\)

`Find substring index` - Returns the index within the source string of the first occurrence of the specified substring.

This action takes in the following input parameters:

* `SourceString` - Source string to search for occurrences in
* `SubString` - Substring to search for in `SourceString` 
* `FromIndex` - Start searching from this index.

`Find substring last index` - Returns the index within the source string of the last occurrence of the specified substring

This action takes in the following input parameters:

* `SourceString` - Source string to search for occurrences in
* `SubString` - Substring to search for in `SourceString` 

`Get substring` - Gets the substring from a string between the start and end indexes.

This action takes in the following input parameters:

* `BeginIndex` - Starting index for the substring
* `EndIndex` - Ending index for the substring
* `InputString` - Input string to search for the substring in

`Calculate string length` - Returns the length of a given string.

The input parameter for this is the string to find the length of, entered into the `InputString` field.

`Replace first substring` - Replaces the first substring of the source string that matches the given regular expression, with the given replacement

This action takes in the following input parameters:

* `SourceString` - Source string
* `Regex` - Regular expression to search for
* `Replacement` - Replacement string \(will replace first occurrence of the result of the regular expression\)

`Replace substrings` - Replaces all substrings in the input string

This action takes in the following input parameters:

* `InputString` - String on which to perform replacements
* `Target` - Sequence to be replaced
* `Replacement` - Substring to replace `Target` with

`Replace substrings with regex` - Replaces all substrings of source string that match the given regular expression with the given replacement

This action takes in the following input parameters:

* `SourceString` - Source string
* `Regex` - Regular expression to search for
* `Replacement` - Replacement string \(will replace all occurrences of the result of the regular expression\)

`Split string with regex` - Splits string around matches of given regular expression

This action takes in the following input parameters:

* `SourceString` - Source string to split
* `Regex` - Regular expression to split around
* `Limit` - Number of strings to get

`String contains` - Checks if the input string contains the given sequence.

This action takes in the following input parameters:

* `InputString` - String to check for substring in
* `Substring` - Substring to search for
* `CaseSensitive` - Indicates if contains search should be case sensitive or not

`String is empty?` - Checks if a given string is empty.

To use this action, specify the input string to check in the`String` input parameter field.

`String starts with?` - Checks if string starts with given prefix

This action takes in the following input parameters:

* `SourceString` - Source string to check if it starts with given prefix
* `Prefix` - Prefix to check for

`Trim string` - Returns new string after removing any leading and trailing whitespace

Provide the string to trim in the `SourceString` input parameter field

