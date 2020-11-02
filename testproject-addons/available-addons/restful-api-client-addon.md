---
description: >-
  This Addon provides actions to to send HTTP/S requests using GET, POST, PUT
  and DELETE methods.
---

# RESTful API Client

## Actions

There are 5 actions in this Addon:

* HTTP GET Request
* HTTP POST Request
* HTTP PUT Request
* HTTP DELETE Request
* HTTP PATCH Request

## Fields

| Field/Action | Required | Input/Output | GET | POST | PUT | DELETE | PATCH |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| uri | X | INPUT | X | X | X | X | X |
| query |  | INPUT | X | X | X | X | X |
| headers |  | INPUT | X | X | X | X | X |
| body |  | INPUT |  | X | X |  | X |
| format |  | INPUT |  | X | X |  | X |
| jsonPath |  | INPUT | X | X | X | X | X |
| expectedStatus |  | INPUT | X | X | X | X | X |
| response |  | OUTPUT | X | X | X | X | X |
| status |  | OUTPUT | X | X | X | X | X |

#### Input Fields

* `uri` - Request URL \(endpoint\)

  > This is a mandatory parameter, otherwise action will fail.

  This parameter should contain only the schema, hostname, path and port \(e.g. [https://domain.tld:8080/api](https://domain.tld:8080/api)\)  
   It should not contain query parameters \(e.g. _?a=1&b=2_\).

* `query` - Query parameters.

  For example:

  If your request query parameters needs to be _a=1_ and _b=2_, then write in this field _a=1&b=2_

  The _&_ symbol is used to separate between each parameter.

* `headers` - Request headers. The following default headers are sent:

  ```text
  accept: text/html, image/gif, image/jpeg, *; q=.2, */*; q=.2
  connection: keep-alive
  content-length: 
  content-type: application/json
  host: The host
  user-agent: Jersey/2.22.1 (HttpUrlConnection 1.8.0_181)
  ```

  > Note: the default headers listed above are not overwritten if you don't specify them.

  The list of headers are separated by commas \(_,_\).

  For example:

  If your request headers needs to be _connection=keep-alive_ and _content-type=application/json_, then write in this field:

  ```text
  connection=keep-alive,content-type=application/json
  ```



  * > Note: You can delimit the headers with a different character by using the **HeaderDelimiter** field.

* `body`- Body that will be sent in the request
* `format`- Body \(if provided\) format. For example: _application/json_ or _text/html_, etc...

  For a complete list of options refer to: [https://en.wikipedia.org/wiki/Media\_type](https://en.wikipedia.org/wiki/Media_type)

* `expectedStatus` - If this parameter is set, the action will check if the **actual** status code equals **expected** status code.

  If the actual status code is not the expected status code then action fail.  
   Accepted values are numbers between 100 and 599 \(1xx - 5xx\).

* `HeaderDelimiter` - This parameter is used to decide the character to delimit the headers around, by default '=' will be used.
* `jsonPath` - This parameter is used to extract nodes or value from server's JSON response \(if such is available\).

  Supported syntax is the _Jayway JsonPath_ syntax.  
   You can find a complete documentation for _Jayway JsonPath_ at [GitHub](https://github.com/json-path/JsonPath)

  For a specific example, see _Example 1.2_

  If the value specified is not found or the the response is a non-JSON response, action will fail.

* `ignoreUntrustedCertificate` - This parameter is used to disable the verification of SSL certificate.

  Parameter is _false_ by default. If set to `true`, RESTful client will accept self signed and untrusted SSL certificate presented by the server when sending a request.

* `schemaValidationOutputFilePath` - This parameter is the file path for the result of the JSON schema validation.

  If empty, it will create the output file in the system's Downloads directory.

* `schemaPath` - This parameter is the path for the JSON Schema file.

  This parameter is for a _full_\* path of a local schema file, or a URL pointing to a remote schema file. If a URL is provided, it will download the schema locally to a temporary file, before performing the validation. Schema validation is performed on the JSON response object provided in the `JsonResponse` field.

* `createFile` - This parameter is a boolean flag to indicate that a validation results output is required.

  If set to `true`, and the `schemaValidationOutput` parameter is set, a file holding the validation result will be created in the provided location.

#### Output Fields

* `response` - The full response from the server or the extracted node/value found using expression specified in `jsonPath` parameter.

  > If `jsonPath` is set, `response` will be limited to the node/value found using the provided expression.  
  >  If the value specified is not found or the the response or the response is not a valid JSON, this field will be empty.

* `jsonResponse` - The full response from the server or the extracted node/value found using expression specified in `jsonPath` parameter as a JSON object.

  > This parameter holds the whole response body, or the node/property requested via jsonPath as a JSON object.

* `status` - Server's response status that is a number between 100 and 599 \(1xx - 5xx\).
* `schemaValidationOutput` - This parameter is the output parameter for the schema validation.

  This parameter will contain the output of any violations in the JSON file according to the provided schema.

## Results

#### Failure Criteria

All actions have several criterions that may result in failure assertion:

* When `expectedStatus` does not match the actual response status:

  > Note: If the `expectedStatus` is not set, and the server responds with status other than 1xx, this will not be considered a failure.

* When the requested node/value by `jsonPath` is not found in the response.
* When server fails to respond.
* Connectivity errors

## Result Description

All actions will report a message with the following information, no matter if the action pass or fail:

* Server response status \(taken from the `status` field\)
* Response body or “No body/value was returned by the server” when it's absent.
* Report of violations discovered using provided json schema, or a statement that none were found.

## Examples

Following TestProject platform conventions, unset parameters will be treated as nulls / empty strings and won't be used.

#### Example 1: POST Request with body

| Field | Value | Input/Output |
| :--- | :--- | :--- |
| uri | [https://jsonplaceholder.typicode.com/posts/1](https://jsonplaceholder.typicode.com/posts/1) | INPUT |
| body | `{"name": "Example User", "email": "a@a.com", "username": "ExampleUser"}` | INPUT |
| response | `{"name": "Example User", "email": "a@a.com", "username": "ExampleUser", "id": 11}` | OUTPUT |
| status | 201 | OUTPUT |

Action result: _PASSED_

#### Example 1.1: POST Request with _expectedStatus_

| Field | Value | Input/Output |
| :--- | :--- | :--- |
| uri | [https://jsonplaceholder.typicode.com/posts/1](https://jsonplaceholder.typicode.com/posts/1) | INPUT |
| body | `{"name": "Example User", "email": "a@a.com", "username": "ExampleUser"}` | INPUT |
| response | `{"name": "Example User", "email": "a@a.com", "username": "ExampleUser", "id": 11}` | OUTPUT |
| status | 201 | OUTPUT |
| expectedStatus | 200 |  |

Action result: _FAILED_ \(Due to `expectedStatus` that does not much `status`\)

#### Example 1.2: POST Request with _jsonPath_

| Field | Value | Input/Output |
| :--- | :--- | :--- |
| uri | [https://jsonplaceholder.typicode.com/posts/1](https://jsonplaceholder.typicode.com/posts/1) | INPUT |
| body | `{"name": "Example User", "email": "a@a.com", "username": "ExampleUser"}` | INPUT |
| jsonPath | name | INPUT |
| response | ExampleUser | OUTPUT |
| status | 201 | OUTPUT |

Action result: _PASSED_

#### Example 2: GET Request

| Field | Value | Input/Output |
| :--- | :--- | :--- |
| uri | [https://jsonplaceholder.typicode.com/posts/1](https://jsonplaceholder.typicode.com/posts/1) | INPUT |
| query | postId=1&id=1 | INPUT |
| response | `{"postId": 1, "id": 1, "name": "SOME_USER_NAME", "email": "SOME_EMAIL", "body": "SOME_BODY"}` | OUTPUT |
| status | 200 | OUTPUT |

Action result: _PASSED_

#### Example 3: DELETE Request

| Field | Value | Input/Output |
| :--- | :--- | :--- |
| uri | [https://jsonplaceholder.typicode.com/posts/1](https://jsonplaceholder.typicode.com/posts/1) | INPUT |
| headers | Authorization=YOUR\_API\_TOKEN,Host=jsonplaceholder.typicode.com | INPUT |
| response |  | OUTPUT |
| status | 200 | OUTPUT |

Action result: _PASSED_

## Valid Schema Format

Below is an example of a valid schema format:

```text
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "$id": "https://reqres.in/api/users?page=2/users.schema.json",
  "title": "users",
  "description": "A user from list",
  "type": "object",
  "properties": {
    "name": {
      "description": "The name for a user",
      "type": "string"
    }
  },
  "required": [ "name" ]
}
```

This is also a good source for a schema: [https://json-schema.org/learn/getting-started-step-by-step.html](https://json-schema.org/learn/getting-started-step-by-step.html)

