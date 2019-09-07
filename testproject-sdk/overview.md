# Overview

TestProject provides a powerful SDK for creating tests and addons using standard open source drivers \(Selenium & Appium\) for Web, Android and iOS applications.

TestProject’s SDK supports standard Selenium and Appium API commands, so you don’t have to change your test logic or learn new APIs if you want to develop tests for web or mobile applications. This makes the development of new tests or porting existing ones as easy and straightforward as possible.

TestProject extends the driver classes by adding extra functionality under the \`testproject\(\)\` property. In a nutshell, in order to get started for a seasoned Selenium/Appium developer, it’s enough to obtain a Driver instance after implementing one of the relevant interfaces, that is injected into the execute\(\) method, from the passed \`helper\` variable, like this: \`helper.getDriver\(\)\`

Currently, TestProject’s SDK has a Java and C\# \(.NET Core\) implementation. Soon, we will provide support for additional programming languages, such as: Python, JavaScript, etc.

