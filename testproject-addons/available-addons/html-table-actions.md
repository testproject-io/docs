# HTML Table Actions

With the [HTML Table actions Addon](https://addons.testproject.io/html-table-actions) you can perform various tasks on HTML tables.

{% hint style="info" %}
The most important thing is to capture the table element in the HTML DOM.
{% endhint %}

This is how you can capture such elements using the [smart test recorder](https://testproject.io/smart-test-recorder/):

* You can either capture the table itself with the element inspector and press double shift:

![Element Inspector in TestProject Recorder](../../.gitbook/assets/html-table-element-inspector.png)

*  Or you can select one of the table cells using the element inspector and press double shift, click on **Parent Element** button and select the table:

![Parent Element in TestProject Recorder](../../.gitbook/assets/parent-element-in-testproject-recorder.png)

Once you've captured the table element, select **Actions**, where you will see all available actions on such element.

Let’s see the available actions for [this addon](https://addons.testproject.io/html-table-actions):

**1.Click on link at a given row (row. Column)**:\
\
Input parameters:

* **Row **– The row where the table cell is located.
* **Column **– The column where the table cell is located.\
  Both of them are zero based (meaning it starts from 0).
* **LinkText  **- The text of the link to be pressed inside the table cell.\
  \
  ** **![](../../.gitbook/assets/html-table-actions-addon-1.png)** ** \


**2. Click on given cell**: This action presses on a given table cell.\
\
Input parameters:

* **Row **– The row where the table cell is located.
* **Column** – The column where the table cell is located.\
  Both of them are zero based (meaning it starts from 0).\
  \
  ** **![](../../.gitbook/assets/html-table-actions-addon-2.png) \


**3. Create CSV file from table**: This action creates a CSV file from the table.

Input parameters (Both Required):

* **NameOfFile **– The name that will be given to the CSV file.
* **LocalPathToFile **– The path where the file will be saved.\
  \
  &#x20;![](../../.gitbook/assets/html-table-actions-addon-4.png) \
  \
  Note: Headers will be the first row of the table.\
  For example, this row in image below will be the headers in the CSV file:

![](../../.gitbook/assets/html-table-actions-addon-3.png)

****\
**4. Search text**:

Input parameter - **TextToSearch**: The text to search inside the table.

![](../../.gitbook/assets/html-table-actions-addon-5.png)

Output parameters:

* **TextFound **– The result if the text was found (true/false).
* **RowIndex **– The row of the cell that contains the text.
* **ColumnIndex** – The column of the cell that contains the text.

![](../../.gitbook/assets/html-table-actions-addon-6.png)



**5. Get Text from a given cell**: This action returns the text contained in a specific table cell

Input parameters:

* **Row **– The row where the table cell is located.
* **Column **– The column where the table cell is located.\
  Both of them are zero based (meaning it starts from 0).

![](../../.gitbook/assets/html-table-actions-addon-7.png)

Output Parameters: **Text **- The text contained in the given cell.

![](../../.gitbook/assets/html-table-actions-addon-10.png)

****

**6. Read entire table**: This action returns the entire text of the table as a comma delimited string.

Output parameter: **TableOutput **– The entire table as a comma delimited string.

![](../../.gitbook/assets/html-table-actions-addon-8.png)

Example:

![](../../.gitbook/assets/html-table-actions-addon-9.png)
