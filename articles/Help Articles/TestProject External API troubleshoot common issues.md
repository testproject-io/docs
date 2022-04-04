---
description: TestProject External API troubleshoot common issues
---

# TestProject External API troubleshoot common issues

When you are getting started with TestProject External API you might come across some errors, this article will troubleshoot common issues when using TestProject API.

### Common fixes: <a href="#h_5f3da989a3" id="h_5f3da989a3"></a>

Did you authorize the page to use the API key? check that you are using an authorization token (API Token) with access to the correct Project.

![](https://downloads.intercomcdn.com/i/o/340730450/3078d2343d9e39fef3515ee4/image.png)

Make sure to change the required data on the example values, the default data is an example of a valid JSON object and will **not** match your details.

![](https://downloads.intercomcdn.com/i/o/340730808/8c02bbdc5f1c366841b66a6d/image.png)

#### 400: Bad request <a href="#h_341392155b" id="h_341392155b"></a>

Make sure to delete the details in the body,

In case you want to use details make sure you provide them in a valid JSON object format.

#### 401: Not authorized <a href="#h_3681c0ade9" id="h_3681c0ade9"></a>

Solution: use the API Key in the lock on the right side.

![](https://downloads.intercomcdn.com/i/o/354977480/7185324b8c2900181491d3ce/image.png)

#### 404: Not found <a href="#h_676d88dcc5" id="h_676d88dcc5"></a>

Solution: your test/project was not found make sure you provided the correct project and test/job IDs.

Also, make sure to check that you have all the required data to execute the request.

#### 201: The execution was queued <a href="#h_a7a318a8f7" id="h_a7a318a8f7"></a>

**This is not an error** - it means the job/test was queued because the agent was busy at the time of the request, the execution was queued and will begin when there are available workers.

\
