# How to change the headless download path

Chrome headless is downloading the file where the **process is launched from.**

Preferences to override this behavior can be found here:

```json
{
 "goog:chromeOptions": {
   "experimentalOptions": {
     "prefs": {
       "download": {
         "default_directory": "C:\\Users\\admin\\Downloads" 
       } 
     } 
   } 
 } 
}
```

For macOS:

```json
{ 
  "goog:chromeOptions": {
    "experimentalOptions": {
      "prefs": {
        "download": {
          "default_directory": "/Users/testproject/Documents" 
        } 
      } 
    } 
  } 
}
```

![](<../../.gitbook/assets/image (457) (1) (1).png>)

Then all you have to do is click save and execute the job you desire with these desired capabilities.
