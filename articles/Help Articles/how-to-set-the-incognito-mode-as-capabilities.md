# How to set the incognito mode as capabilities



You can set the incognito mode as desired capabilities by following this example:

![](<../../.gitbook/assets/image (484).png>)

```json
{  "browserName": "chrome",  "version": 83,  "goog:chromeOptions": {    "args": [      "--incognito"    ]  }}
```
