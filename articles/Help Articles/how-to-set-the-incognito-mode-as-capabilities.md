# How to set the incognito mode as capabilities



You can set the incognito mode as desired capabilities by following this example:

![](https://downloads.intercomcdn.com/i/o/307505362/49384b992e01e51a7466b835/image.png)

```json
{  "browserName": "chrome",  "version": 83,  "goog:chromeOptions": {    "args": [      "--incognito"    ]  }}
```
