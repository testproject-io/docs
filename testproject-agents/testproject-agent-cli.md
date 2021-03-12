---
description: TestProject Agent CLI (Command-Line Interface)
---

# TestProject Agent CLI

TestProject Agent CLI is a cross operating system command line interface utility.  It is made for the execution of test packages generated using the TestProject platform.

These files can be stored outside of the TestProject cloud, including in an on-premises version control such as git.

### Test Packages

A package can be either a single file \(JSON or YAML\) that contains a test, and its auxiliary \(nested and recovery\) tests, or an archive \(ZIP\) that is called a bundle and will contain additional files besides the test itself.

A single file \(JSON or YAML\) doesn't contain any dependencies like apps, coded tests, or addons that are used in the test.  The assumption is that they were already downloaded by the executing Agent or will be downloaded on demand from the TestProject cloud over the internet by the executing Agent before an execution.

A package bundle, on the contrary to a single file, will contain all the dependencies \(apps, coded tests or addons\) and additional files such as settings and parameters for overriding default values and data-driven execution.

#### Package Bundle Structure

The following files tree demonstrates a package bundle structure:

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
├── package.{json/yaml}
├── project-parameters.{json/yaml}
├── settings.{json/yaml}
└── test-parameters.csv
```

## Running the CLI

TestProject Agent CLI allows interaction with the Agent and specifically execution of packages.

CLI can be started from the Agent installation folder or from any other location by executing the following command from the shell:

```text
foo@bar:~$ testproject-agent
```

Or via command prompt / PowerShell in Windows:

```text
testproject-agent.exe
```

When started without parameters or with the `help` parameter, CLI will display self-explanatory usage instructions, e.g.

```text
foo@bar:~$ testproject-agent help
```

Will print:

```text
Usage: testproject-agent [-v] [-a=<agent>] [COMMAND]
  -v, --version         Print version information and exit
Commands:
  start     Starts the Agent
  connect   Connects to an Agent and prints its version
  register  Registers an Agent using provided API or Development token
  browsers  List available browsers
  devices   List and query available devices
  validate  Inspects and validates an execution package file(s)
  run       Runs an execution package file(s)
  help      Displays help information about the specified command
```

Running it with the `-v` or `--version` option will print the TestProject Agent CLI version, e.g.

```text
foo@bar:~$ testproject-agent -v
```

Will print:

```text
2.0.0-RELEASE
```

### Commands

TestProject Agent CLI allows invocation of various features using a command parameter.  The following sections describe all the supported commands.

#### Start

This command allows starting a local Agent. Before CLI attempts to start the Agent, it verifies that no other Agent process is running.

```text
foo@bar:~$ testproject-agent start
```

The command above with no options specified will start the Agent from within the CLI. CLI process will keep running until the Agent quits or is shut down.

Here's the command help:

```text
foo@bar:~$ testproject-agent -h

Usage: testproject-agent start [-fhjsV] [-d=<dataPath>]
Starts the Agent
  -d, --data-path=<dataPath>
                   Path to Agent's data folder
  -f, --fork       Fork current process and exit after Agent is started
  -h, --help       Show this help message and exit.
  -j, --json       Change default output format to JSON
  -s, --headless   Run Agent headless (do not show system tray icon)
  -V, --version    Print version information and exit.
```

**Fork**

Using the `-f` or `--fork` option CLI process can be forked when the Agent process is started.  In this mode, no STD will be attached and CLI will not wait for the Agent to exit.  This might be useful in CI / CD pipelines and various configurations.

#### Connect

This command connects to an Agent and prints its version:

```text
foo@bar:~$ testproject-agent connect
```

Will print:

```text
Agent Version: [1.0]
```

> If there is no Agent running, a relevant error message will appear.

#### Register

This command allows registering an Agent when it is not registered.

> Agent must be running before a registration attempt.  It can be started using the start command if necessary.

Here's the command usage help:

```text
foo@bar:~$ testproject-agent register --help

Usage: testproject-agent register [-hV] -a=<alias> -t=<token>
Registers an Agent using provided API or Development token
  -a, --alias=<alias>   Alias to use when naming the Agent
  -h, --help            Show this help message and exit.
  -t, --token=<token>   Token to use for registration
  -V, --version         Print version information and exit.
```

Notice the `-a` or `--alias` and the `-t` or `--token` required options that should be used to invoke the command properly.  For example right after installation, you can run the following command to register the Agent as _MyAgent_:

```text
foo@bar:~$ testproject-agent register -a MyAgent -t ***
```

**Token**

The token used in the command above \(masked as triple asterisks\) is actually an **API** or a **Development** token.  Any of them can be obtained from the [Integrations](https://app.testproject.io/#/developers/sdk) page on the TestProject platform.

> If the Agent is already registered, a relevant error message will appear.

#### Browsers

This command queries the Agent and provides a list of browsers that are installed on the machine where Agent is running.  It can be used to efficiently configure the execution settings with a list of available browsers for Web test execution.

```text
foo@bar:~$ testproject-agent browsers
```

Running the command shown above will result in an output similar to the below:

```text
+=========+===============+
| type    | version       |
|=========|===============|
| EDGE    | 88.0.705.81   |
| CHROME  | 88.0.4324.192 |
| SAFARI  | 14.0.3        |
| FIREFOX | 85.0          |
+=========+===============+
```

It can be formatted as JSON if an additional option `--json` is set:

```text
foo@bar:~$ testproject-agent browsers --json
```

Will result in:

```javascript
{
  "browsers": [{
    "type": "EDGE",
    "version": "88.0.705.81"
  }, {
    "type": "CHROME",
    "version": "88.0.4324.192"
  }, {
    "type": "SAFARI",
    "version": "14.0.3"
  }, {
    "type": "FIREFOX",
    "version": "85.0"
  }]
}
```

Information about available browsers can be used to configure execution settings.

> Chrome and Firefox have a headless operation mode.  When configuring execution settings, use `CHROME_HEADLESS` and `FIREFOX_HEADLESS` when required.

#### Devices

This command allows listing connected devices \(also Android emulators or iOS simulators\) to an Agent.  It also allows listing Apps installed on a device.

Here's a usage help printout:

```text
foo@bar:~$ testproject-agent devices list --help

Usage: testproject-agent devices list [-hjV] [--android | --ios]
       [--physical | --virtual]
List available devices
  -h, --help       Show this help message and exit.
  -j, --json       Change default output format to JSON
  -V, --version    Print version information and exit.
Mobile Platform
      --android    List only Android devices
      --ios        List only iOS devices
Device Type
      --physical   List only physical devices
      --virtual    List only virtual (emulator or simulator) devices
```

**List**

When the `list` parameter specified, CLI will list devices:

```text
foo@bar:~$ testproject-agent devices list
```

Will result in a similar output to the following:

```text
+======+==========+==========+=======================================+=======================================+=========+
| udid | platform | type     | name                                  | model                                 | version |
|======|==========|==========|=======================================|=======================================|=========|
| ***  | IOS      | PHYSICAL | iPad                                  | MP2G2                                 | 14.4    |
| ***  | IOS      | VIRTUAL  | iPad Pro (11-inch)                    | iPad Pro (11-inch)                    | 12.4    |
| ***  | IOS      | VIRTUAL  | iPhone SE                             | iPhone SE                             | 12.4    |
| ***  | IOS      | VIRTUAL  | iPhone 5s                             | iPhone 5s                             | 12.4    |
| ***  | IOS      | VIRTUAL  | iPhone 6                              | iPhone 6                              | 12.4    |
| ***  | IOS      | VIRTUAL  | iPhone 6 Plus                         | iPhone 6 Plus                         | 12.4    |
| ***  | IOS      | VIRTUAL  | iPhone 6s                             | iPhone 6s                             | 12.4    |
| ***  | IOS      | VIRTUAL  | iPhone 6s Plus                        | iPhone 6s Plus                        | 12.4    |
| ***  | IOS      | VIRTUAL  | iPhone 7                              | iPhone 7                              | 12.4    |
| ***  | IOS      | VIRTUAL  | iPhone 7 Plus                         | iPhone 7 Plus                         | 12.4    |
| ***  | IOS      | VIRTUAL  | iPhone 8                              | iPhone 8                              | 12.4    |
| ***  | IOS      | VIRTUAL  | iPhone 8 Plus                         | iPhone 8 Plus                         | 12.4    |
| ***  | IOS      | VIRTUAL  | iPhone X                              | iPhone X                              | 12.4    |
| ***  | IOS      | VIRTUAL  | iPhone Xs                             | iPhone Xs                             | 12.4    |
| ***  | IOS      | VIRTUAL  | iPhone Xs Max                         | iPhone Xs Max                         | 12.4    |
| ***  | IOS      | VIRTUAL  | iPhone Xʀ                             | iPhone Xʀ                             | 12.4    |
| ***  | IOS      | VIRTUAL  | iPad (5th generation)                 | iPad (5th generation)                 | 12.4    |
| ***  | IOS      | VIRTUAL  | iPad (6th generation)                 | iPad (6th generation)                 | 12.4    |
| ***  | IOS      | VIRTUAL  | iPad Air                              | iPad Air                              | 12.4    |
| ***  | IOS      | VIRTUAL  | iPad Air (3rd generation)             | iPad Air (3rd generation)             | 12.4    |
| ***  | IOS      | VIRTUAL  | iPad Air 2                            | iPad Air 2                            | 12.4    |
| ***  | IOS      | VIRTUAL  | iPad Pro (10.5-inch)                  | iPad Pro (10.5-inch)                  | 12.4    |
| ***  | IOS      | VIRTUAL  | iPad Pro (12.9-inch)                  | iPad Pro (12.9-inch)                  | 12.4    |
| ***  | IOS      | VIRTUAL  | iPad Pro (12.9-inch) (2nd generation) | iPad Pro (12.9-inch) (2nd generation) | 12.4    |
| ***  | IOS      | VIRTUAL  | iPad Pro (12.9-inch) (3rd generation) | iPad Pro (12.9-inch) (3rd generation) | 12.4    |
| ***  | IOS      | VIRTUAL  | iPad Pro (9.7-inch)                   | iPad Pro (9.7-inch)                   | 12.4    |
| ***  | ANDROID  | PHYSICAL | google-pixel_4a-0A301JEC217496        | Pixel 4a                              | 30      |
| ***  | ANDROID  | VIRTUAL  | emulator-5554                         | Android SDK built for x86_64          | 29      |
+======+==========+==========+=======================================+=======================================+=========+
```

There are additional options available to narrow down the list:

* Using the `--android` or `--ios` options, list can be filtered by a mobile platform.
* Using the `--physical` or `--virtual` options, either physical or virtual devices only can be requested.

Another useful option is the `--json`, that will output results as JSON, for example:

```text
foo@bar:~$ testproject-agent devices list --physical --json
```

Will result in a similar output:

```javascript
{
  "devices": [{
    "udid": "***",
    "platform": "IOS",
    "type": "PHYSICAL",
    "name": "iPad",
    "model": "MP2G2",
    "version": "14.4"
  }, {
    "udid": "***",
    "platform": "ANDROID",
    "type": "PHYSICAL",
    "name": "google-pixel_4a",
    "model": "Pixel 4a",
    "version": "30"
  }]
}
```

**Apps**

When the `apps` parameter specified, CLI will list apps installed on a device.  It requires an additional argument `-d` or `--device` to be specified, for example:

```text
foo@bar:~$ testproject-agent devices apps -d ***
```

Assuming the triple asterisks above are an actual UDID of a device, this command will print a list of apps installed on a device with this UDID, for example here's a printout of apps on an Android device:

```text
+============+=========================================+===============================================================+
| name       | packageName                             | activityName                                                  |
|============|=========================================|===============================================================|
| Calculator | com.google.android.calculator           | com.android.calculator2.Calculator                            |
| Calendar   | com.google.android.calendar             | com.android.calendar.AllInOneActivity                         |
| Camera     | com.google.android.GoogleCamera         | com.android.camera.CameraLauncher                             |
| Chrome     | com.android.chrome                      | com.google.android.apps.chrome.Main                           |
| Clock      | com.google.android.deskclock            | com.android.deskclock.DeskClock                               |
| Contacts   | com.google.android.contacts             | com.android.contacts.activities.PeopleActivity                |
| Drive      | com.google.android.apps.docs            | com.google.android.apps.docs.app.NewMainProxyActivity         |
| YouTube    | com.google.android.youtube              | com.google.android.youtube.app.honeycomb.Shell$HomeActivity   |
+============+=========================================+===============================================================+
```

Or something similar for an iOS device:

```text
+===========+===================+=======================================+
| name      | version           | bundleId                              |
|===========|===================|=======================================|
| App Store | 1                 | com.apple.AppStore                    |
| Books     | 4698              | com.apple.iBooks                      |
| Calendar  | 1.0               | com.apple.mobilecal                   |
| Camera    | 3732.0.210        | com.apple.camera                      |
| FaceTime  | 36                | com.apple.facetime                    |
| Family    | 1                 | com.apple.family                      |
| Feedback  | 454               | com.apple.appleseed.FeedbackAssistant |
| Files     | 200.4.1           | com.apple.DocumentsApp                |
| Mail      | 3654.60.0.1.23    | com.apple.MailCompositionService      |
| Maps      | 2608.33.11.29.4   | com.apple.Maps                        |
| YouTube   | 16.05.9           | com.google.ios.youtube                |
+===========+===================+=======================================+
```

Using the `--json` option same output will be presented as a JSON:

```text
foo@bar:~$ testproject-agent devices apps -d *** --json
```

#### Validate

This command inspects the contents of a backup package or bundle, validates it, and prints basic details about it:

```text
foo@bar:~$ testproject-agent validate backup.json
```

Running the command shown above will print similar details:

```text
Package Protocol: 1
Project
+========================+==================+
| ID                     | Project Name     |
|========================|==================|
| ***                    | My First Project |
+========================+==================+

Tests
+========================+==================+
| ID                     | Test Name        |
|========================|==================|
| ***                    | My First Test    |
+========================+==================+
```

> Protocol version indicates what is the TestProject Agent CLI compatible version for this backup file.

Same data can be presented as a JSON if the `--json` the option is used:

```text
foo@bar:~$ testproject-agent validate backup.json --json
```

Will output similar details:

```javascript
{
  "protocol": 1,
  "project": {
    "***": "My First Project"
  },
  "tests": {
    "***": "My First Test"
  }
}
```

#### Run

This command should be used to execute a backup package.  Here are the usage instructions following the execution of the command with the `--help` option:

```text
foo@bar:~$ testproject-agent run --help

Usage: testproject-agent run [-hV] [-rd] [-o=<outputPath>]
                             [-p=<parametersFile>] [-r=<report>]
                             [-s=<settingsFile>] [-d=<servers>]...
                             [--browser=<browsers> [--browser=<browsers>]... |
                             --device=<devices> [--device=<devices>]...]
                             <files>...
Runs an execution package file(s)
      <files>...             Path to execution package file(s)
  -h, --help                 Show this help message and exit.
  -o, --output-path=<outputPath>
                             Output folder path for the local report file(s)
  -p, --parameters=<parametersFile>
                             Parameters file (data-source CSV/YAML)
      --plain                Produce plain output (without progress bars).
  -r, --report=<report>      Report type - local, cloud or both (default)
      -rd, --restart-driver  Restart driver before each test
  -s, --settings=<settingsFile>
                             Execution settings file (targets, etc.)
  -V, --version              Print version information and exit.
Targets
      --browser=<browsers>   Target browsers (multi-value)
      --device=<devices>     Target devices (multi-value)
```

As stated earlier a package can be either a single JSON or YAML file, or an archive \(ZIP\).

**Settings**

A bundle \(ZIP\) is a self-sufficient archive that contains a settings file with a pre-selected list of browsers or devices for execution.  While a stand-alone JSON or YAML file requires to specify these settings.

In order to override execution settings included in a bundle or to specify execution settings for a stand-alone JSON or YAML file, the following options are available:

* `-s` or `--settings` should be used to provide an external setting file.
* `--browser` or `--device` to provide a list of target browsers or devices as command arguments.

The following example demonstrates the execution of a bundle:

```text
foo@bar:~$ testproject-agent run MyFirstTestBackup.zip
```

And this is an example of an _unbundled_ stand-alone YAML:

```text
foo@bar:~$ testproject-agent run MyFirstTestBackup.yaml
```

> Since no setting are bundled, and none are provided, default target will be used.  Chrome or any other installed browser for Web test and any connected device for Mobile.

To override bundled settings using a file, the following command can be executed with `-s` or `--settings` option:

```text
foo@bar:~$ testproject-agent run MyFirstTestBackup.zip --settings settings.yaml
```

The command above will use settings configured in `settings.yaml` instead of the settings inside the archive.  The same could be achieved using the `--browser` option:

```text
foo@bar:~$ testproject-agent run MyFirstTestBackup.zip --browser CHROME --browser FIREFOX
```

The command above will override bundled settings and use provided list of browsers.  In case of a mobile test, device\(s\) UDID\(s\) should be provided using `--device` option:

```text
foo@bar:~$ testproject-agent run MyFirstTestBackup.zip --device *** --device ***
```

Command arguments can also be used to provide settings for _unbundled_ files such as stand-alone JSON or YAML:

```text
foo@bar:~$ testproject-agent run MyFirstTestBackup.yaml --browser SAFARI --browser EDGE
```

**Parameters**

Similar to _settings_, test parameters can be overridden or provided externally.

In order to override bundled test parameters using an external file, `-p` or `--parameters` option should be used:

```text
foo@bar:~$ testproject-agent run MyFirstTestBackup.zip --parameters parameters.csv
```

The same syntax should be used to supply parameters values for an _unbundled_ stand-alone JSON or YAML backup files:

```text
foo@bar:~$ testproject-agent run MyFirstTestBackup.yaml --parameters parameters.csv
```

**Report**

Following an execution, a local report generated.  By default, it will be created under Agent's data folder, inside `reports` folder.

To specify a different location, `-o` or `--output-path` parameter can be used:

```text
foo@bar:~$ testproject-agent run MyFirstTestBackup.zip -o ~/Desktop
```

the command above will run `MyFirstTestBackup.zip` bundle and generate a report in `~/Desktop`, for example:

```text
Executing target 1/1: [Chrome (Headless) 88.0.4324.192]
Tests 100% │██████████████████████████████████████████│ 1/1 (0:00:00 / 0:00:00) 
Steps 100% │██████████████████████████████████████████│ 1/1 (0:00:00 / 0:00:00) 
Execution Report: /Users/testproject/Desktop/{GUID}.html
Execution is complete.
```

In the example above, the report file created in `/Users/testproject/Desktop/MyFirstTest-{TIMESTAMP}.html`

**Progress**

Execution progress is represented using progress bars by default.  For consoles that do not support progress bars representation, please use `--plain` option to output plain text progress.

> Progress does **not** indicate steps results such as passed or failed, but only a periodic indication of the execution advancement. Therefore, when using the `--plain` option, the same step might appear more than once or do not appear at all if execution advances too quickly.

It is also possible that when using progress bars, it will not reach 100% if the test fails on one of the steps before reaching the end. To inspect the actual execution results, refer to the report file generated a the end of the execution.

## Summary

TestProject CLI is a powerful tool allowing the execution of backup packages.  It can be used on-premises and integrated into any CI / CD pipelines.

TestProject CLI is available as part of the TestProject Agent v2.0.0 installation.

