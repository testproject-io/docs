# Create and Schedule Jobs

One important aspect of test automation is being able to run the tests on a regular cadence. Often teams are interested in how the product quality looks as the code changes and so tests need to be run on some kind of schedule. TestProject provides you with the tools that you need to schedule and run tests by adding a job to your project. 

To create a job, navigate to the project you want to add a job for and in the right hand panel click on the Add a job button.

![Add a Job](../.gitbook/assets/image%20%28132%29.png)

This will bring up the job creation wizard. Enter in a name and description for the job and click next. On the next page you can choose where you want the job to run. You can either run a mobile or web test and you can pick which agent you want to use to run the job. Make sure that you are selecting compatible agents for the kind of testing that you want to do. For example, if you want to run the job as a mobile android test, be sure to pick an agent that will have an android device attached. 

![Select job type](../.gitbook/assets/image%20%2871%29.png)

After selecting the job type and clicking Next you will be prompted to pick the device you want to use \(for mobile tests\) or the browser\(s\) you want the job to run on \(for web tests\).

![Select Browsers](../.gitbook/assets/image%20%28106%29.png)

The next step is to pick the schedule that you want the job to run on. The On demand option will create a job for you with the settings that you've picked.  You can then run this job any time you want by pressing the Run Job button. This option is helpful for features that you need to check once in a while, but that may not need to be run on a regular schedule.

You can also setup a job to run just one time. Pick the date and time and TestProject will schedule the job to run then. This option can be helpful for running a test that needs to execute a certain time - perhaps a test that you want to run at night while you are away from your machine. 

The final scheduling option you have is to set the job up to run at a regular recurring time. You can pick the frequency you want for the job and pick the particular time you want for it to run.  For example, you may want to run a set of tests every evening or you may want to run an hourly suite of tests or a weekly suite.  Any of these options can be setup. As you choose options on the picker, pay attention to the text at the bottom that lets you know what the execution time of the job will be so that you can be sure you are setting up the schedule in the way you want.

![Setup up Recurring Schedule](../.gitbook/assets/image%20%287%29.png)

With the schedule setup, you can click on Finish to create the job. This will add the job into the Jobs panel and you can now add any tests from the project into that job. Simply pick the tests you want to add and drag them over to the job and drop them into it. 

You can also setup email notifications for the job by click on the email icon and then choosing if you want to be notified when the job starts, finishes or both. 

![Job Notifications](../.gitbook/assets/image%20%28133%29.png)

If you need to run different tests on different schedules you can create several jobs and set them each up the way that you want, giving you the fine grained control you need over tests executions.

