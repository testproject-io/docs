# Organizing and Managing Test Data

Test Data is important to any test automation effort, but as an application gets bigger and more tests are added, test data management becomes more difficult. There are a few tools that you can use within TestProject to help with this.

## Elements

Elements make up the core of any test automation effort and so within each project TestProject helps you organize and manage them. Any elements you use in a test are automatically added to the elements for that project. The project management area lets you create different folders to organize your test elements. One way to organize elements could be to have a folder for each application you are testing and then create a subfolder under there for each page of the application. &#x20;

![Creating folders for your applications pages](<../../.gitbook/assets/image (460) (1).png>)

Elements can be easily moved to different folders by dragging and dropping them.

![Organizing the recorded elements in the different folders](<../../.gitbook/assets/image (457) (2).png>)



You can also move them to another folder by using the more menu.&#x20;

![Using the menu to move elements to a folder](<../../.gitbook/assets/image (459) (1).png>)

Keeping structure and organization like this in place will help make test maintenance easier and make it a lot easier to work together and collaborate as a team on the ongoing work of test automation

## Tests

Tests themselves are an important part of the data that needs to be maintained in a test automation initiative. As with elements, tests can also be organized and placed into folders. You can use this to structure tests into logical areas that make it easy to decide which tests to run and to set up and [schedule ](../../schedule-and-run-tests/create-and-schedule-jobs.md)them into the jobs that you want.

![Creating Test Folders](<../../.gitbook/assets/image (463) (1) (1).png>)

In the same way as with elements, tests can be moved to a different folder by either using drag and drop or by using the Move to folder option on the more menu for the test.&#x20;

## Parameters

TestProject makes it very easy to parameterize tests and so it is important to consider how to manage and organize parameters within the system. Parameters can be set up and either the test level or the project level. More details on how to effectively use them can be found in the section of the documentation on the [effective use of parameters](using-parameters-effectively.md).
