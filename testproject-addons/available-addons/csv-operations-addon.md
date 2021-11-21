# CSV Operations Addon

This addon provides actions for working with CSV files. You can use this addon to create CSV files during your test execution, merge two CSV files, export a CSV file to JSON file, etc. This addon is also useful for exporting parameters to CSV file during the test execution.

### Available Actions

`Append values to a CSV file` - Appends new values to an existing CSV file

This action has the following inputs:

* `Values`- Specify the values. Values are separated by your chosen delimiter and each row is separated by a new line
* `Path` - Path to where you want the CSV file to be stored on the local machine
* `Delimiter` - The character you want to use to separate the values (e.g. comma, semi-colon etc.). The same delimiter should be used to separate values in the `Values` field

`Create a new CSV file` - Creates a CSV file from a given string of values

This action requires the following inputs:

* `Names` - Specify the column names as a list. Separate each item on the list with your choosen delimiter (for example, commas)
* `Values`- Specify the values. Values are separated by your chosen delimiter and each row is separated by a new line
* `Path` - Path to where you want the CSV file to be stored on the local machine
* `FileName` - The name you want to give the file
* `Delimiter` - The character you want to use to separate the values (e.g. comma, semi-colon etc.). The same delimiter should be used to separate values in the `Names` and `Values` fields

`Delete a column from a CSV file by index` - Deletes a column from a CSV file at the specified index

This action requires the following inputs:

* `Path` - Full path to the locally stored CSV file (e.g. C:\Temp\myFile.csv)
* `Index` - The index of the column you wish to delete from the file. The index starts from zero

`Export CSV file to json` - Opens a CSV file and writes the contents of the file into a json string

This action requires the following inputs:

* `CsvPath` - Full path to the locally stored CSV file (e.g. C:\Temp\myFile.csv)
* `FileName` - The name of the json file that will be stored on your local machine
* `JsonPath` - Path on your local machine where you want to save the json file

`Merge two CSV files` - Merges a new CSV file to an existing CSV file

This action requires the following inputs:

* `OldFile` - Path to the CSV file you wish to append to (e.g. C:\Temp\old.csv)
* `NewFile` - Path to the CSV file to add to the other file (e.g. C:\Temp\new.csv)

`Reverse the order of a CSV file` - Reverses the order of the provided CSV file. This action takes in one input

* `Path` - Path to the locally stored CSV file (e.g. C:\Temp\myFile.csv

`Read CSV row` - Read the entire data of a given row.

* `filePath` - Path to the CSV file you wish to read (e.g. C:\Test\test.csv)
* `row `- the index other the row to read (starts from 1)

`Read CSV column` - Read the entire data of a given column.

* `filePath` - Path to the CSV file you wish to read (e.g. C:\Test\test.csv)
* `column`- the index other the column to read (starts from 1)

As of version **4.0** of the addon, you are able to specify the **encoding **of the CSV file being read and written to with an additional optional field.

* `fileEncoding`

By default, the encoding used will be UTF-8 and supports others such as UTF-8, UTF-16, UTF-16LE, UTF-16BE, US-ASCII, ISO-8859-1etc.

