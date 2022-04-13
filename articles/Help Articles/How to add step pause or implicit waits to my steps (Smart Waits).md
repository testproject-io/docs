# How to add step pause or implicit waits to my steps (Smart Waits)

Just like in Selenium and Appium, TestProject supports explicit and implicit waits for steps in a test.

#### Define step pause (Explicit Wait) <a href="#define-step-pause-explicit-wait" id="define-step-pause-explicit-wait"></a>

The driver will wait for a given amount of time before or after the step execution. In TestProject, it's called "Step Pause".\


#### Implicit wait <a href="#implicit-wait" id="implicit-wait"></a>

Can also be referred as "Smart Wait". The driver will try to execute the step for a defined amount of time (timeout). If the step was executed successfully before the timeout exceeded, the test will continue to the next step. In case the timeout exceeded, the step will be reported as failed.

You can find both of these waits in the Smart Recorder step editor as seen below:\


![](https://downloads.intercomcdn.com/i/o/170672799/56755a964b34d2d7c4842756/A2pIKiySWO.png)

![](<../../.gitbook/assets/image (549).png>)
