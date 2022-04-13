---
description: Get text and type text using TestProject recorder - Control C / Control V
---

# Copy and Paste text during a test

Sometimes you will need to copy text from your application and paste it somewhere else, or you will need to copy a text and use it for comparison later.

In that case, you will need to use [Test Parameters](https://docs.testproject.io/getting-started/create-a-test-step/using-parameters-in-test-steps). to achieve a full copy and paste follow these steps:

First, get the text and add that to the parameter:﻿

![](../../.gitbook/assets/b1100e38b00520a5c63abdcd13fc7083e2aa2e11\_2\_690x324.png)

Like this:

![](../../.gitbook/assets/4b55418900bdcc18bfc20b5554773415a32d0372\_2\_284x500.png)

Create a parameter:

![](<../../.gitbook/assets/f2309fb58653ba0c7e5f691da267974f7540bdda (1).png>)

Name it, and then leave the default value empty if it's dynamically assigned during the test.

![](<../../.gitbook/assets/image (461) (1) (1) (1).png>)

Select your parameter:

![](<../../.gitbook/assets/image (463) (2).png>)

And Save the step:\
﻿

![](<../../.gitbook/assets/image (472) (2).png>)

Now to use it hover over the element and use double "SHIFT" to open the element inspector in the field Actions choose Type text action:\
﻿

![](<../../.gitbook/assets/image (469) (1) (2).png>)

\
﻿Then choose the text parameter that you have created:\
﻿

![](<../../.gitbook/assets/image (455) (1) (2).png>)

Select this:

![](<../../.gitbook/assets/image (473) (2).png>)

\
﻿and save the step:\
﻿

![](<../../.gitbook/assets/image (475) (2).png>)

\
﻿So now you can run your flow and save text into a parameter and type or use it as you want.\
﻿

![](<../../.gitbook/assets/image (476) (1) (2).png>)

\
﻿The text will be taken, assigned into the parameter, and then typed on the field:\
﻿

![](<../../.gitbook/assets/image (474) (1) (2).png>)

_**NOTE:**_

_If you want to save the value of the parameter and use it in a different test you should create a Project Parameter and use it instead of the Test Parameter._

_Project parameters keep their assigned values outside of execution._
