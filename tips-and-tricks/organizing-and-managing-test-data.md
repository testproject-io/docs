# Organizing and Managing Test Data

Test Data is important to any test automation effort, but as an application gets bigger and more tests are added, test data management becomes more difficult. There are a few tools that you can use within TestProject to help with this.

## Elements

Elements make up the core of any test automation effort and so within each project TestProject helps you organize and mange them. Any elements you use in a test are automatically added to the elements for that project. The project management area lets you create different folders to organize your test elements. One way to organize elements could be to have a folder for each application you are testing  and then creating sub folder under there for each page of the application.  



![Elements](https://lh3.googleusercontent.com/6ZwY8uQjKB3aC2Su0QBn-_qFdG16Ui7V7kZQ186Jfol5sumqNUr-hX_K-xN9vmotR1ZM43IStangmllI7Sp8CVf8LRW-tXmtz7pQR0UcHTOHNUNL7enN6gfhwlYJKYT-Vqfh9WCyWraAIg)

Elements can be easily moved to different folders by dragging and dropping them. You can also move them to another folder by using the more menu. 

![Move to folder](../.gitbook/assets/image%20%28194%29.png)

Keeping structure and organization like this in place will help make test maintenance easier and make it a lot easier to work together and collaborate as a team on the ongoing work of test automation

## Tests

Tests themselves are an important part of the data that needs to be maintained in a test automation initiative. As with elements, tests can also be organized and placed into folders. You can use this to structure tests into logical areas that make it easy to decide which tests to run and to setup and [schedule ](../schedule-and-run-tests/create-and-schedule-jobs.md)them into the jobs that you want.

![Test Folders](../.gitbook/assets/image%20%28132%29.png)

In the same way as with elements, tests can be moved to different folder by either using the drag and drop mechanism, or by using the Move to folder option on the more menu for the test. 

## Parameters

TestProject makes it very easy to parameterize tests and so it is important to consider how to manage and organize parameters within the system. Parameters can be setup and either the test level or the project level. More details on how to effectively use them can be found in the section of the documentation on the [effective use of parameters](using-parameters-effectively.md).

