---
description: TestProject SDK For Addons
---

# Creating an Addon

This article covers getting started with creating addons using the Java SDK.

## Getting Started

To get started, you need to complete the following prerequisites checklist:

* Login to your account at [https://app.testproject.io/](https://app.testproject.io) or [register](https://app.testproject.io/signup/) a new one.
* [Download](https://app.testproject.io/#/download) and install an Agent for your operating system or pull a container from [Docker Hub](https://hub.docker.com/r/testproject/agent).
* Run the Agent and [register](https://docs.testproject.io/getting-started/installation-and-setup#register-the-agent) it with your Account.
* Download [Java SDK for Addons](https://app.testproject.io/#/integrations/develop-addon)

### Installation

The open source version (v2) of the SDK does not yet support addon creation, so you will need to add the downloaded SDK as a dependency in your `pom.xml` file. This article will show you how to do that in Eclipse, but you can of course follow similar steps in whichever IDE you are using.&#x20;

In an Eclipe project, make sure that you have a `lib` folder and if not add one to your project. Copy the Java SDK file that you [downloaded ](https://app.testproject.io/#/integrations/develop-addon)from TestProject, into that folder. You should see something like this in  Eclipse:

![TestProject SDK](<../../.gitbook/assets/image (411).png>)

Once you have done that, you can right click on the SDK file and choose the properties option. This will show you the **Location** of the SDK. Copy that location and then edit your `pom.xml` file  and add the following dependecy into it:

```markup
<dependency>
    <groupId>io.testproject</groupId>
    <artifactId>java-sdk</artifactId>
    <version>1.0</version>
    <systemPath>/path/to/sdk/TestProject_SDK_0.65.0.jar</systemPath>
    <scope>system</scope>
</dependency>
```

You will of course, need to set the `systemPath` entry to the location that you copied the SDK into.

If you hare working with a Gradle project, you can add the dependency by adding the following to your `build.gradle` file:

```java
 compile files("/path/to/sdk/TestProject_SDK_0.65.0.jar")
```

Where once again the path is the location that you copied earlier.&#x20;

If you want to see more details, you can look at the `pom.xml` and `build.gradle`files in the [examples ](https://github.com/testproject-io/addons/tree/master/Examples)of the addons github repository.

## Addon development

In order to get started with developing and Addon, you will need a manifest file. This file contains a descriptor of your addon, which includes a unique GUID for the addon and a list of the permissions that the addon will need. TestProject will automatically generate this file for you.

### Generating an Addon Manifest

In order to generate a manifest file, you will need to login to the [TestProject App](https://app.testproject.io) and then go the addons tab. Click on the Create Addon button:

![Create Addon Button](<../../.gitbook/assets/image (413).png>)

On the resulting dialogue, give your addon a name. For this article we will implement a simple addon that gives us the ability to clear the fields on a form, so you can name it something like **ClearFieldsExampleAddon**. Click next and you can optionally give some additional details like the source code and documentation links if you have them. Click **Next** again and you can choose what permission your addon needs. In this example, you should not need any special permission, so you can leave them unselected and just click on the **Generate and Download Manifest** button to create the manifest.

![Generate and Download Manifest](<../../.gitbook/assets/image (412).png>)

{% hint style="warning" %}
We will return to this dialog in a few minutes, keep it open for now
{% endhint %}

Once the manifest has downloaded, you will need to add it to the resources folder in your project. If you do not yet have that folder, add it under `src/main`. If you are using Eclipse, it should look something like this:

![Manifest File in Eclipse](<../../.gitbook/assets/image (410).png>)

Now that you have the manifest file and the proper dependencies, you are ready to start implementing an addon.

### Implement the Addon

Lets look at implementing the code for a simple Addon with a **ClearFields** action that clears a form. In order to do this, you will need to create a package in Eclipse. On the `src/main/java` folder, right-click and under new, choose **Package**. Name the package something like _io.testproject.myaddon_ and click **Finish**. You can then add a class to that package by right-clicking on it and going to new>Class. Name the class something like _ClearFieldsAction_ and click on **Finish**. __ You can then fill in the following code to create the addon.

```java
package io.testproject.myaddon;

import io.testproject.java.annotations.v2.Action;
import io.testproject.java.sdk.v2.addons.WebAction;
import io.testproject.java.sdk.v2.addons.helpers.WebAddonHelper;
import io.testproject.java.sdk.v2.drivers.WebDriver;
import io.testproject.java.sdk.v2.enums.ExecutionResult;
import io.testproject.java.sdk.v2.exceptions.FailureException;
import org.openqa.selenium.By;
import org.openqa.selenium.WebElement;

@Action(name = "Clear Fields")
public class ClearFieldsAction implements WebAction {

    public ExecutionResult execute(WebAddonHelper helper) throws FailureException {

        // Get Driver
        WebDriver driver = helper.getDriver();

        // Search for Form elements
        for (WebElement form : driver.findElements(By.tagName("form"))) {

            // Ignore invisible forms
            if (!form.isDisplayed()) {
                continue;
            }

            // Clear all inputs
            for (WebElement element : form.findElements(By.tagName("input"))) {
                element.clear();
            }
        }

        return ExecutionResult.PASSED;
    }
}
```

This addon will find all element on a page that have the `form` tag (unless the form is not being displayed) and clear any data that is in those form fields.

## Packaging

It really is that easy to create your own addon, but you in order to use it in the test recorder you will need to upload it to the TestProject app. In order to do that, you have to first package it as JAR file. When you package up your code, do so as an `uber-jar` file with dependencies, excluding the TestProject SDK. If you are working with a Maven package, you can do this by adding the following to the `pom.xml` file.

```markup
<build>
    <plugins>
        <!-- Assembly Plugin - Create a JAR with dependencies for uploading to 
        TestProject -->
        <plugin>
            <artifactId>maven-assembly-plugin</artifactId>
            <configuration>
                <descriptors>
                    <descriptor>src/main/descriptor.xml</descriptor>
                </descriptors>
            </configuration>
            <executions>
                <execution>
                    <id>make-assembly</id>
                    <phase>package</phase>
                    <goals>
                        <goal>single</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>
        <!-- Compile Plugin -->
        <plugin>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.5.1</version>
            <configuration>
                <source>1.8</source>
                <target>1.8</target>
            </configuration>
        </plugin>
    </plugins>
</build>
```

As you can see in the code above, the `maven-assembly-plugin` is going to look at the file `src/main/descriptor.xml` to find out what assemblies to generate. If you don't have that file yet, you can go ahead and create it from the right-click menu on the `src/main` folder. Choose **new>File** and naming the file _descriptor.xml._ Add the following `xml` into the file and save it:

```markup

<?xml version="1.0" encoding="UTF-8"?>
<assembly>
        xmlns="https://maven.apache.org/plugins/maven-assembly-plugin/assembly/1.1.0"
        xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="https://maven.apache.org/plugins/maven-assembly-plugin/assembly/
        1.1.0 http://maven.apache.org/xsd/assembly-1.1.0.xsd">
    <id>jar-with-dependencies</id>
    <formats>
        <format>jar</format>
    </formats>
    <includeBaseDirectory>false</includeBaseDirectory>
    <dependencySets>
        <!--Assemble all runtime dependencies-->
        <dependencySet>
            <outputDirectory>/</outputDirectory>
            <useProjectArtifact>true</useProjectArtifact>
            <unpack>true</unpack>
            <scope>runtime</scope>
        </dependencySet>
        <!--Extract TestProject SDK Properties-->
        <dependencySet>
            <outputDirectory>/</outputDirectory>
            <useProjectArtifact>true</useProjectArtifact>
            <scope>system</scope>
            <unpack>true</unpack>
            <includes>
                <include>io.testproject:java-sdk</include>
            </includes>
            <unpackOptions>
                <includes>
                    <include>testproject-sdk.properties</include>
                </includes>
            </unpackOptions>
        </dependencySet>
        <!--Exclude TestProject SDK from the resulting JAR-->
        <dependencySet>
            <outputDirectory>/</outputDirectory>
            <unpack>true</unpack>
            <scope>system</scope>
            <excludes>
                <exclude>io.testproject:java-sdk</exclude>
            </excludes>
        </dependencySet>
    </dependencySets>
</assembly>
```

This file provides the information maven needs in order to assemble all the dependencies for the jar file along with the SDK properties, while excluding the SDK itself from the jar file.

Once you have these files created and saved, you can run the commands to package it up. First make sure everything in maven is up to date, by going to **Maven** on the right click menu and choosing the **Update Project** option. You can then make sure everything is ready by going to **Run As** on the right click menu and choosing **Maven Clean.** Once you run that choose the Maven build option ensuring that the **Goal** is set to _package_.  This should create the jar files that you need and if you refresh the package, you should see jar files in the target folder of your package.

![Generated Addon Files](<../../.gitbook/assets/image (416).png>)

You will need to upload the `jar-with-dependencies.jar` file to TestProject which you can see how to do in the [next section](./#uploading-the-addon-to-testproject).

If you prefer to build with gradle, you can use the following build.gradle file to package your addons, just update the **TP\_SDK** variable to the correct location of the TestProject SDK on your system.

```java
group 'io.testproject'
version '1.0.1'

apply plugin: 'java'

// Update the location of TestProject SDK JAR file
def TP_SDK = "__PATH_TO_LOCAL_JAR__/io.testproject.sdk.java.jar"

compileJava.options.encoding = 'UTF-8'

sourceCompatibility = 1.8

repositories {
    mavenCentral()
}

// Configurations
configurations {
    tpsdk
    compile.extendsFrom tpsdk
}

// JAR Task
jar {
    assert file("${TP_SDK}").exists() : "TestProject SDK JAR file was not found, please update the TP_SDK variable"
    archiveName "${rootProject.name}-${version}.jar"
    dependsOn configurations.runtime
    from {
        // Removes TestProject SDK from the final jar file
        (configurations.runtime - configurations.tpsdk).collect {
            it.isDirectory() ? it : zipTree(it)
        }
    }

    // Extract SDK version
    from {
        (configurations.tpsdk).collect {
            zipTree(it).matching {
                include 'testproject-sdk.properties'
            }
        }
    }
}

dependencies {
    tpsdk files("${TP_SDK}")
}
```

## Uploading the Addon to TestProject

Once you have packaged up the addon, you can add it into the TestProject application. Go back to the TestProject application and click Next on the dialog. You can then upload the file.

![Upload Addon File](<../../.gitbook/assets/image (418).png>)

Once the file has uploaded, click **Next** and then review your actions to make sure everything looks good.

![Review Addon Actions](<../../.gitbook/assets/image (414).png>)

Click Finish and the addon will be created in your TestProject account. You can go to the Addon page and then click on My Addons to see the addon you just uploaded.

![New Addon](<../../.gitbook/assets/image (415).png>)

And that is all it takes!  You can now start using the actions in this addon while making recorded tests. If you create a recorded test that loads the https://example.testproject.io/web page and enters some text into the form, you can then add a step to the test and search for the addon. In this case, since you are using the same addon that is used in other examples, you might see multiple instances of it. If you mouse-over the addons, you will be able to see which one is yours and choose it.&#x20;

![Add a step using your addon](<../../.gitbook/assets/image (417).png>)

If you are not yet familiar with the test recorder, you can checkout the section in the docs on [getting started with creating a web test](../../using-the-smart-test-recorder/web-testing/introduction-to-web-testing.md).  This simple example shows you how to get started, but there are many different options available when creating your own Addons. Check out the[ next section](addon-action-options.md) of the documentation to see the details of the kinds of things you can do when creating addons.
