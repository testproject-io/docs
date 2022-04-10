# How to create a dynamic date picker

First record the select day step:

![](https://testproject-5b5666821ab7.intercom-attachments-1.com/i/o/491260803/8c68d80ef5ed6660fcaad525/a8bfc5e0533a639528454308ccf72ea94c1ae34d\_2\_690x454.png)

then, go into the click step and change the day to a parameter in the locator:

![](https://testproject-5b5666821ab7.intercom-attachments-1.com/i/o/491260817/1cb8285f3759ea75550f9db9/d4d1a5b8ad625d855987cec7739df91aa4fd5aa4.png)

![](https://testproject-5b5666821ab7.intercom-attachments-1.com/i/o/491260827/84709d2f0062e757ba2cebf3/3af4ae2f3cf0a026cf111cda553b907598b0fd09.png)



\
﻿You need to delete all the locators and leave only the first one with the parameter so they do not affect the selection of the element.\
﻿Now, let’s create the parameter so we can make the selection dynamic:

![](https://testproject-5b5666821ab7.intercom-attachments-1.com/i/o/491260837/d732770f955c32a5b013ec72/384b06ef0bfa631ea1e31e1c3ba80e2b83cb3737.png)

Create the parameter for the day:

![](https://testproject-5b5666821ab7.intercom-attachments-1.com/i/o/491260843/5da0aa0c0ceebbdfc253cd34/f6fbcd9abedbd154a7662fc0c9a18f248c43302b.png)

I chose the default day to be 1.

![](https://testproject-5b5666821ab7.intercom-attachments-1.com/i/o/491260850/6dc070b27d425277baeafc3f/2f4c0c7f4c6f904e7afbb67eb5d0b25b0894a76a.png)

You can select another value for this parameter from the parameter tab to 20 to, just for the example.

![](https://testproject-5b5666821ab7.intercom-attachments-1.com/i/o/491260859/01aa84b67cec30883a7108f2/1d8504970851d336433b45d22faa8b0c58979573.png)

Once I have the parameter I can do data-driven testing and so in each iteration, I will select other dates.

for more info about the data-driven testing you can go [here](https://docs.testproject.io/using-the-smart-test-recorder/using-data-driven-jobs-in-testproject).
