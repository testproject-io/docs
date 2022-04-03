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

![](https://downloads.intercomcdn.com/i/o/473744718/09f4aa1161804856e2d8fcfe/chrome\_O3py5oa3lR.png)

* After we have provided the authentication with the API key, we can start and fill the inputs with the correct values and click on the execute button.

![](https://downloads.intercomcdn.com/i/o/473750641/978800546d880eebb329e663/chrome\_aOyknwwXOi.png)

* Now after we provided these details and executed we should get a request URL, the server response is "400" and that's fine because the package file needs to be sent as an “application/octet-stream” body and that's what we are going to do in Postman, this is the request URL that we'll copy:

![](https://downloads.intercomcdn.com/i/o/473754834/0f1efb0c34f854c645eb8747/chrome\_iUfrVd9pwe.png)

### How to execute correctly this URL from Postman: <a href="#h_ec132b65cf" id="h_ec132b65cf"></a>

* First, we'll paste the request URL and it should provide and create for us the Params automatically (If it didn't provide for you automatically you can just copy and paste the keys and paste your value):

![](https://downloads.intercomcdn.com/i/o/473766603/aa2a666c021e6fae05e833ec/Postman\_5x0SYo9giJ.png)

* Now we'll have to fill the Headers section, in the authorization you have to provide the API key, and in the content type fills the value: application/octet-stream:

![](https://downloads.intercomcdn.com/i/o/473770066/58955f4e8d366079806e762d/Postman\_z5lVbMFUT7.png)

* In the body section, we will select binary and it will let us select a file so all you have to do is to select your jar file and open him there:

![](https://downloads.intercomcdn.com/i/o/473772076/3927a7b6ff1140d613c5f303/Postman\_PqSrWcqOn7.png)

* And that's it you can execute this request and navigate back to your project and see the new coded file package:

![](https://downloads.intercomcdn.com/i/o/473774887/0be2dd5a6007e78195bfb52f/chrome\_IR8E0ZrNMH.png)

**Note: the selected jar file must have the same file name you provided in TestProject API documentation.**
