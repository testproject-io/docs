# How to Execute Tests from Outside the Test Recorder

The TestProject Test Recorder is a powerful and versatile tool that let's you easily create, edit and run tests. However, it is not the only way to interact with tests from within TestProject. You can run tests directly from the Test Recorder, but they can also be run in several other ways.

## Running Tests in a Project

If you navigate to a project with tests, you can run those tests directly from the project folder. Doing this is as simple as mousing over the test you are interested in and then click on the run icon.

![Run Tests from Project](../.gitbook/assets/image%20%28128%29%20%281%29.png)

When you do that, you will be prompted to pick the test agent and browser or device that you want to run the test on. If the test has parameters defined, you will then have the option to override those parameters if you want. You can also at this point import or use a data source to set your test parameters \(see[ the documentation on data driven testing ](../schedule-and-run-tests/using-data-driven-jobs-in-testproject.md)for more details on how this works\).

Once you have set the options you want and clicked on Run, TestProject will open the browser or device you selected and run the test. After the test completes, you can go to the reports tab, to look at the details of the test run.

## Running Tests with Jobs

You can also run tests in TestProject using [Jobs](../schedule-and-run-tests/create-and-schedule-jobs.md). Jobs allow you to organize and schedule the running of tests and are a powerful way to create schedules for your tests and give you control over the frequency and timing of running your tests.

Jobs different combinations of tests and are easy to create directly in the TestProject application. They are a powerful tool to help you with running tests.

## Running Tests in CI

Tests can also be from outside of the TestProject app. For example, you can run tests in you CI with Jenkins by following the documentation [here](../testproject-integrations/integration-with-jenkins.md). You can also run tests that you have developed with an SDK. For example the [C\# SDK](../testproject-sdk/opensdk-v2/c-sdk.md) documentation shows you how to setup running tests that you have developed in this way. 

There are many ways to run tests from within TestProject. You can run tests directly in the test recorder, from the project page, as part of a job or even from outside of the TestProject app. No matter what your needs are for running tests, TestProject has a way to do it that you can use.

