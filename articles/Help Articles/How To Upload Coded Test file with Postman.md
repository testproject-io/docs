---
description: >-
  A practical guide on how to upload coded tests from postman using TestProject
  API
---

# How To Upload Coded Test file with Postman

### How to get the correct URL endpoint: <a href="#h_388c50d93c" id="h_388c50d93c"></a>

*   First, we'll have to navigate to TestProject API documentation and get to the specific post request endpoint the name is "Create Coded Test package file" you can get directly to the endpoint by clicking this link:

    [https://api.testproject.io/docs/v2/#/TestPackages/TestPackages\_CreateTestPackageAsync](https://api.testproject.io/docs/v2/#/TestPackages/TestPackages\_CreateTestPackageAsync)
* After we got there we'll have to provide an API key for authorization:

![](<../../.gitbook/assets/chrome\_O3py5oa3lR (1).png>)

* After we have provided the authentication with the API key, we can start and fill the inputs with the correct values and click on the execute button.

![](<../../.gitbook/assets/chrome\_aOyknwwXOi (1).png>)

* Now after we provided these details and executed we should get a request URL, the server response is "400" and that's fine because the package file needs to be sent as an “application/octet-stream” body and that's what we are going to do in Postman, this is the request URL that we'll copy:

![](<../../.gitbook/assets/chrome\_iUfrVd9pwe (1).png>)

### How to execute correctly this URL from Postman: <a href="#h_ec132b65cf" id="h_ec132b65cf"></a>

* First, we'll paste the request URL and it should provide and create for us the Params automatically (If it didn't provide for you automatically you can just copy and paste the keys and paste your value):

![](<../../.gitbook/assets/Postman\_5x0SYo9giJ (1).png>)

* Now we'll have to fill the Headers section, in the authorization you have to provide the API key, and in the content type fills the value: application/octet-stream:



![](<../../.gitbook/assets/Postman\_z5lVbMFUT7 (1).png>)

* In the body section, we will select binary and it will let us select a file so all you have to do is to select your jar file and open him there:

![](../../.gitbook/assets/Postman\_PqSrWcqOn7.png)

* And that's it you can execute this request and navigate back to your project and see the new coded file package:

![](../../.gitbook/assets/chrome\_IR8E0ZrNMH.png)

**Note: the selected jar file must have the same file name you provided in TestProject API documentation.**
