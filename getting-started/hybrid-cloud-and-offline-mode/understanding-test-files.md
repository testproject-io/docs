# Understanding Test Files

You can download tests from the TestProject platform to run them locally. 

![Save a test locally](../../.gitbook/assets/image%20%28116%29.png)

When you download these tests, the information is stored in a `.yaml` file. YAML is a human-readable format for describing structured data. Once you have downloaded the files locally, you can open them in a text editor and see information about the test. The `.yaml` file for each test stores information about the test that will allow it to run, however, you can also download a test package that will include additional information about how to run the test.

### Test Packages

A package is an archive \(`.zip`\) that contains additional files besides the test itself. While the single test `.yaml` file doesn't contain any dependencies like apps, coded tests, or addons that are used, test packages include all of these things. It will also include additional files such as settings and parameters for overriding default values and data-driven execution.

#### Package Bundle Structure

The following file tree demonstrates a package bundle structure:

```text
package.zip
├── addons
│   ├── {addon-guid}
│   ├── {addon-guid}
│   ├── {addon-guid}
├── apps
│   ├── {app-guid}.{ipa/apk}
│   ├── {app-guid}.{ipa/apk}
│   ├── {app-guid}.{ipa/apk}
├── coded-tests
│   ├── {test-guid}.{jar/dll/zip}
│   ├── {test-guid}.{jar/dll/zip}
│   ├── {test-guid}.{jar/dll/zip}
├── package.{yaml}
├── project-parameters.{yaml}
├── settings.{yaml}
└── test-parameters.csv
```

The `addons` folder will contain information about any addons that your tests use. This information is not human readable, but is used by the TestProject agent to load and run those addons without needing to connect to the TestProject cloud.

Similarly the `apps` folder contains information about any apps that you may have defined to be used in your tests and the `coded-tests` folder contains any compiled coded tests that the test uses. 

There are also several `.yaml` files that are used to define the test and some settings for it. The `package.yaml` file defines the details of the test including things like it's name and the various test steps and actions that each step will take along with the elements it will act on. This file on its own is enough for running many tests and can be executed via the [TestProject CLI](../../testproject-agents/testproject-agent-cli.md). 

The `project-parameters.yaml` file contains information about project level parameters. When setting up tests in TestProject you can[ define parameters](../create-a-test-step/using-parameters-in-test-steps.md) for various inputs and outputs. These parameters can be defined directly in a test, and in that case they will be stored in the `package.yaml` file. However, it is also possible to define paramters that are saved in a project and shared between multiple tests. Information about these parameters will be stored in the `project-parameters.yaml` file. 

In addtion, a test package includes a `settings.yaml` file. This file defines what browsers and devices you want the test to run on. You can manually modify this file to change those settings, or you can override them with the command line interface. 

If your test does have parameters defined, the package will also include a file called `test-parameters.csv` which contains the values for the parameters. If you want, you can add additional parameters to this file to run the test in a data driven manner. 



