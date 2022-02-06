---
description: Documentation for XLSX Operations addon
---

# XLSX Operations

This addon provides actions for working with XLSX files. You can use this addon to analyze and check XLSX files during your test execution, compare two XLSX, search for values, etc.&#x20;

### Available Actions

#### Generic Actions (any file)

`Wait for file download`

`Delete file (if exists)`

* Path is required.

#### XLSX Actions

`Compare two XLSX files`

`Get cell value`

`Get the sum of a column`

`Get the value of a column`

`Get the row value`

`Search value and replace it in Excel file`

`Search value in Excel file`

`Search index value of header in Excel file`

`Set value to a cell in excel file`



* All XLSX actions accept a **path** and the path must end with XLSX, for example: `"C:\Temp\workbook.xlsx"`
* Sheet is optional, if the sheet is not provided the action will default to use the **first shee**t in the workbook.
* All other parameters are **required**.
* The result for the operation can be validated on the output field.
* Search and replace actions will match all the results found in the workbook and should be used cautiously, an index of the row and column for the desired match can be extracted from the output.

