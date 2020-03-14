# RESTful API Client Addon

Many applications have APIs that allow the manipulation of parts of the application without using the user interface. Integration these kinds of calls into your tests can sometimes make them much more efficient and powerful. The RESTful API Client Addon provides actions to to send HTTP/S requests using REST based GET, POST, PUT, PATCH and DELETE API methods.  

Each of these methods provides several different fields.

###  **Input Fields:**

**`uri`** - Request URL \(endpoint\)

> Note that this is a mandatory parameter, otherwise action will fail.

The uri parameter should contain only the schema, hostname, path and port \(e.g. [https://domain.tld:8080/api](https://domain.tld:8080/api)\) and should not contain query parameters \(e.g. _?a=1&b=2_\).

**`query`** - Query parameters.

Query parameters need to be specified as `queryName = queryvalue`. If you have multiple query parameters in one call they need to be separated by the `&` symbol. So for example if you have 2 query parameters that need to be `a=1` and `b=2` then fill in this field as `a=1&b=2`

**`headers`** - Request headers.  By default the following headers are sent:

```text
accept: text/html, image/gif, image/jpeg, *; q=.2, */*; q=.2
connection: keep-alive
content-length: 
content-type: application/json
host: The host
user-agent: Jersey/2.22.1 (HttpUrlConnection 1.8.0_181)
```

> Note: the default headers listed above are not overwritten if you don't specify them.

You can add or modify headers by specifying them in the headers field. The list of headers are separated by commas \(_,_\).

For example, if your request headers needs to be _Accept-Encoding: \*_ and _content-type:application/xml_, then write in this field:

```text
Accept-Encoding=*,content-type=application/xml
```

`body`- Body that will be sent in the request 

This parameter is only relevant for POST and PUT requests. It can be specified in formats like json or text, with the format being declared in the format field

`format`- Body \(if provided\) format. For example: _application/json_ or _text/html_, etc...

For a complete list of options refer to: [https://en.wikipedia.org/wiki/Media\_type](https://en.wikipedia.org/wiki/Media_type)

`expectedStatus` - If this parameter is set, the action will check if the **actual** status code equals **expected** status code.

If the actual status code is not the expected status code then action fail. Accepted values for this field are numbers between 100 and 599 \(1xx - 5xx\).

`jsonPath` - This parameter is used to extract nodes or value from server's JSON response \(if such is available\). Supported syntax for this field is the _Jayway JsonPath_ syntax which you can find a complete documentation for on [GitHub](https://github.com/json-path/JsonPath)

If the value specified is not found or the the response is a non-JSON response, the action will fail.

`ignoreUntrustedCertificate` - This parameter is used to disable the verification of SSL certificate.

Parameter is _false_ by default. If set to `true`, RESTful client will accept self signed and untrusted SSL certificate presented by the server when sending a request.

### **Output Fields**

`response` - The full response from the server or the extracted node/value found using expression specified in `jsonPath` parameter.

> NOTE: If `jsonPath` is set, `response` will be limited to the node/value found using the provided expression. If the value specified is not found or the the response or the response is not a valid JSON, this field will be empty.

`status` - Server's response status that is a number between 100 and 599 \(1xx - 5xx\).

### Results

#### **Failure Criteria**

All actions have several criterion that may result in the test step failing:

* When `expectedStatus` does not match the actual response status:

  > Note: If the `expectedStatus` is not set, and the server responds with status other than 1xx, this will not be considered a failure.

* When the requested node/value by `jsonPath` is not found in the response.
* When server fails to respond.
* Connectivity errors

#### Result Description

All actions will report a message with the following information, regardless of if the action passes or fails:

* Server response status \(taken from the `status` field\)
* Response body or “No body/value was returned by the server” when it's absent.

### **Further Resources**

Further documentation and examples can be found [here](https://github.com/testproject-io/addons/tree/master/restful-api-client) on github where you can also see the code for this addon. 



