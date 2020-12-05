# Individual Run Reports

TestProject [provides a number of built-in plots](types-of-plots-in-testproject-reports/) that provide nice summaries of the tests that you have run, but it does more than that. It also gives you drill down reports for each test or job that you run.  These reports are crammed full of information that can help you when you are trying to figure out why a test failed and also contain a lot of useful information for summary reports.

## Debugging Test Failure

If you run a test and it fails, you can go to the report for that test run. To do that go to the Reports tab and then click on the project that the test belongs to. TestProject will show you the summary charts of the test runs for that project but if you want to see the results of an individual test run you can easily do that by clicking on the job or test run in the left-hand navigation tree.

![Navigation Tree](../.gitbook/assets/image%20%28103%29.png)

Select the test you are interested in and you should see a summary of the test run showing you details like the agent that rand the test, and the time it took to run the test along with a summary of how many tests passed or failed. The is also a link on this panel that allows you to download PDF reports. You can either download just the summary, or if you want, the detailed step-by-step report.

![Test Run Summary](../.gitbook/assets/image%20%28115%29.png)

The right hand panel shows you the test steps that were executed. Any failed steps will be marked with a red bar and if you click on them to expand that test step, TestProject will show you some additional details about the failure. You will see a summary of the action that test step was trying to perform and a message indicating what went wrong. If you have screen shots enabled for you test you will also see the screen shot for the failing test, which you can click on to expand.

![Failing Test Step](../.gitbook/assets/image%20%28114%29.png)

The right-hand panel also has an option that you can toggle to show only failing test steps which can be helpful if you have a lot of test steps to look through.

![Show only Failed Test Steps](../.gitbook/assets/image%20%28100%29.png)

### Self-healing Test Reports

Test Project also has self-healing capabilities built in and so if it cannot find an element it will automatically attempt to alternative element locators. When it does so, it lets you know in the reports by showing a beating heart icon to indicate that the test has been automatically healed. 

![Self-healed Test Icon](../.gitbook/assets/image%20%28175%29.png)

The description for that step in the report will also let you know which selector it switched to when it healed the test.

![Self-healed test Information](../.gitbook/assets/image%20%28174%29.png)



