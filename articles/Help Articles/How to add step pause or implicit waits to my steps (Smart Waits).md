# How to add step pause or implicit and explicit waits to my steps (Smart Waits)

Just like in Selenium and Appium, TestProject supports explicit and implicit waits for steps in a test.

#### Define execution speed (Explicit Wait) <a href="#define-step-pause-explicit-wait" id="define-step-pause-explicit-wait"></a>

The driver will wait for a given amount of time before or after the step execution. In TestProject, it's called "execution speed".\


![](<../../.gitbook/assets/image (502).png>)

#### Implicit wait (adaptive wait) <a href="#implicit-wait" id="implicit-wait"></a>

The driver will try to execute the step for a defined amount of time (timeout). If the step was executed successfully before the timeout exceeded, the test will continue to the next step. In case the timeout exceeded, the step will be reported as failed.

You can find both of these waits in the Smart Recorder step editor as seen below:\


![](<../../.gitbook/assets/image (549).png>)

#### "Pause" step <a href="#implicit-wait" id="implicit-wait"></a>

Another option is to add manually a "PauseYou can add use the "Pause" action. This is how you can add it:

![](https://downloads.intercomcdn.com/i/o/459159019/7e42513e1526bd21c50f9e77/image.png)



![](https://downloads.intercomcdn.com/i/o/459159371/a7bf8fe0888c754b090c0757/image.png)



![](https://downloads.intercomcdn.com/i/o/459159754/74f086a9e8451d896653965b/image.png)
