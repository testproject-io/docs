# Understanding Test Files

You can download tests from the TestProject platform to run them locally.&#x20;

![Save a test locally](<../../.gitbook/assets/image (219).png>)

When you download these tests, the information is stored in a `.yaml` file. YAML is a human-readable format for describing structured data. Once you have downloaded the files locally, you can open them in a text editor and see information about the test. The `.yaml` file for each test stores information about the test that will allow it to run, however, you can also download a test package that will include additional information about how to run the test.

### Test Packages

A package is an archive (`.zip`) that contains additional files besides the test itself. While the single test `.yaml` file doesn't contain any dependencies like apps, coded tests, or addons that are used, test packages include all of these things. It will also include additional files such as settings and parameters for overriding default values and data-driven execution.

#### Package Bundle Structure

The following file tree demonstrates a package bundle structure:

```
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

Similarly the `apps` folder contains information about any apps that you may have defined to be used in your tests and the `coded-tests` folder contains any compiled coded tests that the test uses.&#x20;

There are also several `.yaml` files that are used to define the test and some settings for it. The `package.yaml` file defines the details of the test including things like it's name and the various test steps and actions that each step will take along with the elements it will act on. This file on its own is enough for running many tests and can be executed via the [TestProject CLI](../testproject-agent-cli.md).&#x20;

The `project-parameters.yaml` file contains information about project level parameters. When setting up tests in TestProject you can[ define parameters](../../using-the-smart-test-recorder/create-a-test-step/using-parameters-in-test-steps.md) for various inputs and outputs. These parameters can be defined directly in a test, and in that case they will be stored in the `package.yaml` file. However, it is also possible to define paramters that are saved in a project and shared between multiple tests. Information about these parameters will be stored in the `project-parameters.yaml` file.&#x20;

In addtion, a test package includes a `settings.yaml` file. This file defines what browsers and devices you want the test to run on. You can manually modify this file to change those settings, or you can override them with the command line interface.&#x20;

If your test does have parameters defined, the package will also include a file called `test-parameters.csv` which contains the values for the parameters. If you want, you can add additional parameters to this file to run the test in a data driven manner.&#x20;

## Upload test Files to TestProject

In addition to downloading files and interacting with them locally, you can also upload test files back into the TestProject cloud if you want. If you have made some changed to a file and want to share that with someone else on your team, you can upload the file into the TestProject application to enable the seamless team collaboration options.&#x20;

In order to do that, simply click on the arrow beside **Open File** button and choose the Import Test option.

![Import Test](<../../.gitbook/assets/image (296).png>)

Then select the test file that you want to upload and click **Import**. This will import the test into the currently selected project.

### Modifying local tests

You can also choose to start from an existing test and edit it, by choosing the Open File button directly.

![Open a file for Editing](<../../.gitbook/assets/image (344).png>)

In that case, after uploading the test file, you will be given the option to start the test recorder or edit the test. You can make any changes that you want and then **Save** the changes to save an updated local file with the new changes included.

