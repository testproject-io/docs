---
description: Java OpenSDK
---
# Java

## Getting Started

Before getting started with using the TestProject Java SDK, there are a few things you need to have in place:

1. Ensure that you have setup everything that you necessary in the prerequisites checklist. You can find that checklist in the [Getting Ready to Use an SDK ](../../overview/getting-ready-to-use-an-sdk.md)section of the documentation.
2. When using the Java SDK, you must also have the Java Development Kit (JDK) 11 or newer installed on your machine. If you do not have JDK installed, you can download and install the latest version from the Oracle website by following the **JDK Download** link on [the oracle Java page](https://www.oracle.com/ca-en/java/technologies/javase-downloads.html).
3. You can work with your Integrated Development Environment (IDE) of choice, but if you are new to developing tests through an SDK, we would recomend that you use Eclipse. This is an open source IDE that has great support for Java. You can download it from the [Eclipse website](https://www.eclipse.org/downloads/) and then insall it setup of Java Development

You will also need a way to add the TestProject SDK into your project. You can do this in several ways, but the most common ways in Java are with Maven or Gradle. These are software tools that help you manage your Java projects and automate your builds.

## Installing the SDK

You can install the SDK in a couple of ways. In this section we will go over the different choices that you have and show you how to use them. If you want to install it using Maven, continue on in the [next section](./#setting-up-maven). If you want to install with Gradle, you can skip ahead to [that section](./#installing-with-gradle).

### Setting up Maven

If you want to install with Maven, you will of course need to have Maven installed on your computer.If you do not yet have it, you can download it from [here](https://maven.apache.org/download.html) and you can find install instructions for it [here](https://maven.apache.org/install.html).

### Creating a Project in Eclipse

In this documentation we will show you how to get started with creating a project in Eclipse. If you are using a different IDE, you should be able to modify these steps to work with your IDE.

Let's look at how to create a new Maven project in Eclipse:

1. Go to File>New and select the **Other** option from the list.
2. Type **Maven** in the filter field and choose the **Maven Project** option.
3. Click **Next.**
4. Select the **Create a simple project** option and click **Next** again.
5. Put in a Group Id and Artifact Id and click Finish.

![Example Project Setup](<../../../.gitbook/assets/image (381).png>)

Now that you have a Maven project, you will need to add the TestProject SDK as a dependency in the `pom.xml` file for your project.

If you expand the project in the navigation tree in Eclipse, you will see the `pom.xml` file and you can double click to open it in for editing.

![pom.xml file](<../../../.gitbook/assets/image (380).png>)

You will need to add a `<dependencies>` section to the file and then add the TestProject dependency:

```xml
<dependencies>
  <dependency>
    <groupId>io.testproject</groupId>
    <artifactId>java-sdk</artifactId>
    <version>1.2.3-RELEASE</version>
  </dependency>
</dependencies>
```

{% hint style="info" %}
Make sure to set the `<version>` to the name of the latest TestProject SDK version. You can find the list of versions in the Maven repository [here](https://search.maven.org/artifact/io.testproject/java-sdk).
{% endhint %}

You don't have to use testing frameworks, but they usually make life a lot simpler, so if you do not yet have one, you might want to also add the following dependency to your `pom.xml`file to add the junit4 test framework into your project.

```xml
<dependency>
     <groupId>junit</groupId>
     <artifactId>junit</artifactId>
     <version>4.13</version>
</dependency>
```

Once you have added the dependencies into the `pom.xml` files you will need to build your package so that the dependencies get installed. Eclipse should automatically rebuild for you as soon as you save your `pom.xml` file. If it doesn't go to This will install the TestProject Java SDK and all it's dependencies for you. Once the build has completed you will see a Maven Dependencies folder in your project and you should be ready to start creating tests in your project!

![](<../../../.gitbook/assets/image (382).png>)

### Installing with Gradle

If you prefer to build with a gradle project, you can do that as well. As with using Maven, we will show you how to do it in Eclipse:

1. Go to File>New and select the **Other** option from the list.
2. Type **Gradle** in the filter field and choose the **Gradle Project** option.
3. Click **Next** and if you get the Welcome page, click **Next** again.
4. Name your project and click **Finish** 

Once you've done this, find the `build.gradle` file in your project and add the following into the dependencies section.

```groovy
implementation 'io.testproject:java-sdk:1.2.3-RELEASE'
```

Note that the Gradle addon usually comes installed with Eclipse. If you are using a different IDE you might need to install Gradle which you can do from [here](https://gradle.org). If Eclipse did not install it, you can go the Help>Ecliple Marketplace and search for **gradle** and install the Buildship Gradle Integration addon.

## Creating Tests With the SDK

Once you have the SDK installed, you can start creating tests with it. If you are familiar with using the Selenium driver, this will feel very familiar since using a TestProject inherits all of the commands from Selenium and Appium and does not override them with any proprietary commands. Generally speaking, the only thing you will need to do differently is to change the `import` statement to use the TestProject SDK, rather than the Selenium based import.

> The following examples are based on the `ChromeDriver`. However they are applicable to any other supported driver, just change the name as appropriate for the browser you are using.

### Creating a Test from Scratch

There are a few different ways to create tests. Let's start with looking at how you can create something like this from scratch. You can do this in Eclipse by going to the `src/tests/java` folder and then right clicking and selecting **Package** from the New menu.

![Create a new Package](<../../../.gitbook/assets/image (379).png>)

Name this package something like _TestProjectDemo_ and click **Finish**. This will create a new project for you, and you can right click on this project and select **Class** from the new menu to create a new class. Name the class _WebTest_ and click **Finish**.

This creates a class file that you can type your code into. Replace the contents of that file with the following code:

```java
package TestProjectDemo; //change this name, if you named your package something else

import io.testproject.sdk.drivers.web.ChromeDriver;
import org.openqa.selenium.By;
import org.openqa.selenium.chrome.ChromeOptions;

public class WebTest {

    public static void main(final String[] args) throws Exception {
        ChromeDriver driver = new ChromeDriver(new ChromeOptions());

        driver.navigate().to("https://example.testproject.io/web/");

        driver.findElement(By.cssSelector("#name")).sendKeys("John Smith");
        driver.findElement(By.cssSelector("#password")).sendKeys("12345");
        driver.findElement(By.cssSelector("#login")).click();

        boolean passed = driver.findElement(By.cssSelector("#logout")).isDisplayed();
        if (passed) {
            System.out.println("Test Passed");
        } else {
            System.out.println("Test Failed");
        }

        driver.quit();
    }
}
```

This creates a test, but you aren't quite ready to run the test yet. You will need to first configure a development token before you can run this example.

## Development Token

In order to run tests, the TestProject agent on your machine needs to be able to communicate with the TestProject platform. This communication channel needs to be authorized with a development token. You can get a dev token from the [sdk/integrations](https://app.testproject.io/#/integrations/sdk) page in the TestProject. The development token can be specified in a few different ways:

### Saving Development Token in Environment Variable

The different drivers in the tests will search for the developer token in an environment variable called`TP_DEV_TOKEN`. If you want to use this method for specifying your token, add an environment variable with this name to your system, and set the value of it to contain your development token.

### Explicitly Providing the Development Token

You can also explicity provide the development token when calling the driver constructor. If you use this option, you can pass in your token as an argument to the constructor. So instead of just setting the `ChromeOptions()` when creating a new driver, you can also specify the token as a string. If you wanted to take this approach, Line 10 in the example above would be replaced with something like this:

```java
ChromeDriver driver =  new ChromeDriver("your token", new ChromeOptions());
```

You of course, need to put in the value for your development token so that it can authenticate you correctly.

### Driver Builder

Another option you have is to use the generic driver builder that the SDK provides. For example, you could construct a `ChromeDriver` with the following code:

```java
ChromeDriver driver = new DriverBuilder<ChromeDriver>(new ChromeOptions())
  .withRemoteAddress(new URL("http://localhost:8585"))
  .withToken("your token")
  .build(ChromeDriver.class);
```

## Running a Test with the SDK

Now that you have specified a development token, you should be able to run the test! In Eclipse all you need to do is click the green run button on the toolbar. When you do that, a Chrome browser will load and it will open the [https://example.testproject.io/web](https://example.testproject.io/web) page and do the actions indicated in the test. Once it is done you should see the words **Test Passed** printed in the console in Eclipse. Don't worry if there are a few warnings in there. As long as you see Test Passed printed, everything should be ok.

{% hint style="info" %}
If the test does not run, check the Console tab in Eclipse. You may see an exception in there saying that it could not connect to the agent. You will need to start up the agent on your local machine before you can run the tests.
{% endhint %}

And there you have it! You have created and run a test with the TestProject SDK. That was pretty easy wasn't it?

## Viewing Reports

By default the TestProject SDK reports all driver commands and their results to the TestProject Cloud. This allows you to see beautifully designed reports and statistics in the TestProject app dashboards.

If you login to the [TestProject App](https://app.testproject.io) and mouse over the Reports menu item, you should see the SDK run that you just did listed there.

![SDK Run in Recent Reports](<../../../.gitbook/assets/image (389).png>)

You can click on this to go to the report for this test run. This will show you all the details of the run.

## Uploading Tests to TestProject

The TestProject SDK automates and simplifies a lot of the work for you, but if you want to fully leverage all the capabilities of the TestProject applicaiton, including things like collaborating on tests with your coworkers and running across mulitple platforms, you will want to upload the coded tests that you create into the application. In order to do that, you will have to build a package that can be uploaded.

You can build packages in a few different ways. You will probably want to use either Maven or Gradle depending on which on you originally installed the SDK with.

### Building a Package with Maven

If you are building with Maven, you can add the following `build` section to your `pom.xml` file

```xml
<build>
    <plugins>
        <!-- Use maven-jar-plugin to include tests -->
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-jar-plugin</artifactId>
            <executions>
                <execution>
                    <goals>
                        <goal>test-jar</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>
        <!-- Use maven-assembly-plugin plugin with a custom descriptor -->
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-assembly-plugin</artifactId>
            <configuration>
                <descriptors>
                    <!-- Path to the descriptor file -->
                    <descriptor>src/main/java/assembly/test-jar-with-dependencies.xml</descriptor>
                </descriptors>
            </configuration>
            <executions>
                <execution>
                    <phase>package</phase>
                    <goals>
                        <goal>single</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>
    </plugins>
</build>
```

The maven assembly plugin references a descriptor file. With the example we are working through in this tutorial, you will not yet have that file. You will need to create it. In order to do that in Eclipse, right click on the `src/main/java` folder in your project and from the **New** menu choose the **Folder** option. Name the folder `assembly` and then right click on it and from the **New** menu select the **File** option. Name this file `test-jar-with-dependencies.xml` and paste the following text into this file:

```xml
<assembly xmlns="http://maven.apache.org/plugins/maven-assembly-plugin/assembly/1.1.0"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xsi:schemaLocation="http://maven.apache.org/plugins/maven-assembly-plugin/assembly/1.1.0 http://maven.apache.org/xsd/assembly-1.1.0.xsd">
    <id>test-jar-with-dependencies</id>
    <formats>
        <format>jar</format>
    </formats>
    <includeBaseDirectory>false</includeBaseDirectory>
    <dependencySets>
        <dependencySet>
            <outputDirectory>/</outputDirectory>
            <useProjectArtifact>true</useProjectArtifact>
            <useProjectAttachments>true</useProjectAttachments>
            <unpack>true</unpack>
            <scope>test</scope>
        </dependencySet>
    </dependencySets>
</assembly>
```

Make sure that you have save the changes to all files that you've edited and then click on the project in the Package Explorer and refresh it. You can either right click and choose the refresh option, or just hit `F5` to refresh. Next, you will want to refresh Maven to make sure everything is up to date. You can do that by right clicking on the project, and going to **Maven** and then choosing the **Update Project** option.

![Update Maven Project](<../../../.gitbook/assets/image (386).png>)

On the resulting popup, ensure that the correct project is selected and then choose the **Force Update of Snapshots/Releases** option. Click on Ok and the project should refresh. Once that has completed, you are ready to run a Maven build.

Click on the `pom.xml` file and then click the green run button on the top menu bar and choose **Maven build**. You might be prompted to create a launch configuration. If you are, set the value of the **Goals** field to _package_ and then click **Run**. Once that completes, you can right click on the package and select refresh to update the view. You should now see some files under the target folder in the Package Explorer.

![Creating Packaged Files](<../../../.gitbook/assets/image (390).png>)

If you want to find out where the file is located on your hard drive, you can right click on the file that ends with `-with-dependencies.jar` and go to **Show In>System Explorer** to open the system explorer at the location of the file.

### Uploading Coded Test to TestProject

Now you can upload the file to TestProject if you want. Go to the project page in the TestProject application and click on the **New Test** button. **Browse** to the location of the file that you created, and **upload** it. Once the upload has completed, you should be able to click on the **Next** button. Give your package a name. In this case something simple as this is just a test

![Package name](<../../../.gitbook/assets/image (394).png>)

Click **Next** again and then click **Start Testing**.

You can now run and share your test within the TestProject application in the same ways that you can interact with the recorded tests in the system.

{% hint style="info" %}
Note that if you need to make changes to the test, you will need to modify the code locally and then upload a new version to update the test in the TestProject application. This action can easily be accessed via the menu on the test, as shown in the image below.
{% endhint %}

![Upload a new version of a coded test](<../../../.gitbook/assets/image (392).png>)

With that you are ready to create your own coded tests!
