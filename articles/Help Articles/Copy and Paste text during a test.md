---
description: Get text and type text using TestProject recorder - Control C / Control V
---

# Copy and Paste text during a test

Sometimes you will need to copy text from your application and paste it somewhere else, or you will need to copy a text and use it for comparison later.

In that case, you will need to use [Test Parameters](https://docs.testproject.io/getting-started/create-a-test-step/using-parameters-in-test-steps). to achieve a full copy and paste follow these steps:

First, get the text and add that to the parameter:﻿

![](https://testproject-5b5666821ab7.intercom-attachments-1.com/i/o/403146287/57d6ebc7a5330bf5d63a3d83/b1100e38b00520a5c63abdcd13fc7083e2aa2e11\_2\_690x324.png)

Like this:

![](https://testproject-5b5666821ab7.intercom-attachments-1.com/i/o/403146318/655111b3790808c183af1e30/4b55418900bdcc18bfc20b5554773415a32d0372\_2\_284x500.png)

Create a parameter:

![](https://testproject-5b5666821ab7.intercom-attachments-1.com/i/o/403146341/4697aa7daa85b463f51128a4/f2309fb58653ba0c7e5f691da267974f7540bdda.png)

Name it, and then leave the default value empty if it's dynamically assigned during the test.

![](https://testproject-5b5666821ab7.intercom-attachments-1.com/i/o/403146348/2848a430f7a0b985cb4fa369/012289b0f23346d815d2a8102a229ebe2616141f.png)

Select your parameter:

![](https://testproject-5b5666821ab7.intercom-attachments-1.com/i/o/403146355/aab78e63528e06b15de8c6d6/2492da399e0e5918dce873df46b57f2654b40ed4.png)

And Save the step:\
﻿

![](https://testproject-5b5666821ab7.intercom-attachments-1.com/i/o/403146360/8e16f17c6f69b16aeb123b74/17e90f3b2132abd01a7f3f11e0c46bd58260fd2f.png)

Now to use it hover over the element and use double "SHIFT" to open the element inspector in the field Actions choose Type text action:\
﻿

![](https://testproject-5b5666821ab7.intercom-attachments-1.com/i/o/403146367/535882e46438ef9624a3646f/8ecaa637c5e3b6352b566b991f4be7160e2d5679\_2\_690x215.png)

\
﻿Then choose the text parameter that you have created:\
﻿

![](https://testproject-5b5666821ab7.intercom-attachments-1.com/i/o/403146380/676a764fd2fe62bebfb77311/0bf1150f78d9c6b69dfa5c5407b96bc1b1aacad1\_2\_281x500.png)

Select this:

![](https://testproject-5b5666821ab7.intercom-attachments-1.com/i/o/403146386/2babd0d4a7eecc4de5b8aa0e/54bfaa8cd0827b279ef67739a15d9c4f4734f39c.png)

\
﻿and save the step:\
﻿

![](https://testproject-5b5666821ab7.intercom-attachments-1.com/i/o/403146401/a798b32afa3c1bc19fc1eb27/4a982a8694c54367608a924ec18342d018a6d699\_2\_287x500.png)

\
﻿So now you can run your flow and save text into a parameter and type or use it as you want.\
﻿

![](https://testproject-5b5666821ab7.intercom-attachments-1.com/i/o/403146410/3ad372cfd114daae9e1eb0eb/c10861bf937b5758ce00522495f23235092f01e8.png)

\
﻿The text will be taken, assigned into the parameter, and then typed on the field:\
﻿

![](https://testproject-5b5666821ab7.intercom-attachments-1.com/i/o/403146421/7820ce3422df0be3edbbd8f4/3fed8a6f44db20c5cfb91e1346d088de69542128\_2\_690x369.png)

_**NOTE:**_

_If you want to save the value of the parameter and use it in a different test you should create a Project Parameter and use it instead of the Test Parameter._

_Project parameters keep their assigned values outside of execution._
