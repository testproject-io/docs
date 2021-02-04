# Step output validations

Many actions return output to the test in the form of Output parameters

![](../.gitbook/assets/image%20%28228%29.png)

We do validations on the returned value. Click on add validation under Validations section

![](../.gitbook/assets/image%20%28231%29.png)

Select the output field and validation type and insert the value you want to compare the fiel to as fixed value or as parameter 

![](../.gitbook/assets/image%20%28229%29.png)

![](../.gitbook/assets/image%20%28230%29.png)

**Available validations:**

| Validation Name | Validation Summary |
| :--- | :--- |
| Starts with | Check if a string output starts with the validation value |
| Ends with | Check if a string output ends with the validation value |
| Contains | Check if a string output contains the validation value |
| Equals | Check if a string or a number output is equal to the validation value |
| Not equals | Check if a string or a number output is not equal to the validation value |
| Greater than | Check if a number output is greater than the validation value |
| Greater than or Equals | Check if a number output is greater than or equals to the validation value |
| Less than | Check if a number output is less than validation value |
| Less than or Equals | Check if a number output is less than or equals to the validation value |
| RegEx | Validate the output field by regex \(Requires entire output string to match, e.g. '^' at the start of the string and '$' at the end\) |

