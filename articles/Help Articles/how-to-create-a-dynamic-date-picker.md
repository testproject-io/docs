# How to create a dynamic date picker

First record the select day step:

![](../../.gitbook/assets/a8bfc5e0533a639528454308ccf72ea94c1ae34d\_2\_690x454.png)

then, go into the click step and change the day to a parameter in the locator:

![](../../.gitbook/assets/d4d1a5b8ad625d855987cec7739df91aa4fd5aa4.png)

![](<../../.gitbook/assets/image (526).png>)

\
﻿You need to delete all the locators and leave only the first one with the parameter so they do not affect the selection of the element.\
﻿Now, let’s create the parameter so we can make the selection dynamic:

![](<../../.gitbook/assets/image (455) (1).png>)

Create the parameter for the day:

![](<../../.gitbook/assets/image (533).png>)

I chose the default day to be 1.

![](<../../.gitbook/assets/image (495).png>)

You can select another value for this parameter from the parameter tab to 20 to, just for the example.

![](<../../.gitbook/assets/image (499).png>)

Once I have the parameter I can do data-driven testing and so in each iteration, I will select other dates.

for more info about the data-driven testing you can go [here](https://docs.testproject.io/using-the-smart-test-recorder/using-data-driven-jobs-in-testproject).
