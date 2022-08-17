---
description: Using the REST addon to perform basic authentication.
---

# RESTful Basic Authentication using TestProject

First of all, if you need to perform API calls using TestProject during your recorded tests you will need to install the RESTful API Client addon.\
This addon provides actions to to send HTTP/S requests using GET, POST, PUT and DELETE methods.

If a client makes a request to a URL for which the server expects authentication information. Most web clients handle this response by requesting a user ID and password from the end user like seen in the following example:

![](<../../.gitbook/assets/image (542).png>)

In order to perform basic authentication you will need to fill in the **Headers** field of the appropriate action like so:\
\
**Authorization= Basic user:pass**

You will need to convert the user:pass part of the field to base64 using an online converter such as [https://www.base64encode.org/](https://www.base64encode.org/) or our Base64 Encoder-Decoder addon.

An example of conversion:\
\
**Before conversion**\
Authorization = Basic David:123456\
\
**After conversion**\
Authorization = Basic RGF2aWQ6MTIzNDU2

The end result should look something like so:

![](<../../.gitbook/assets/image (538).png>)

![](<../../.gitbook/assets/image (479).png>)

Where it can be seen that what appears after Basic is the encoded character string.
