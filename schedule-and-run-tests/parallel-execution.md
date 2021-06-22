---
description: Executing tests in parallel on a single Agent
---

# Parallel Execution

## Parallel Execution

Parallel execution is a new feature introduced in TestProject version **3.0**.  It is a very powerful feature, that can take your test automation a huge leap forward by reducing the testing time significantly.  TestProject is the only platform that provides parallel execution capabilities for free without limitations.

#### What is serial testing?

Before answering the question of what parallel testing is, first let's define and understand what _serial testing_ is.

_Serial testing_ is a method wherein tests are running one after another, meaning that a previous test must finish before another one gets started. So for example, if a test execution time on average is one minute, executing ten \(10\) tests, with different parameter values, will require ten minutes!

Running the same ten tests on different browsers, e.g. Chrome, Firefox, Edge, etc. will require half an hour, and sometimes these tests should be verified on mobile browsers or with other permutations introduced: device/browser/version and parameters values \(data sources\).

Thus the time needed grows exponentially, making the automation a bottleneck.

Today, QA teams have to run the tests across all environments and scenarios. Cross-browser and cross-device testing is a key requirement. To achieve this goal efficiently, time-saving parallel testing is required.

#### What is parallel testing?

_Parallel testing_ is a test automation method wherein test cases are simultaneously run on multiple combinations of browsers, operating systems, and devices \(including Android emulators and iOS Simulators\). Parallel testing increases the testing speed and allows faster time to market.

### Agent Workers Configuration

A parallel task, also known as an _Agent Worker_, can be a test/job execution, a recording session or an OpenSDK development session.

Running tests and jobs in parallel requires additional resources and capabilities from the machine they are running on.  It is not reasonable to spawn hundreds of browsers simultaneously, therefore please make sure that this setting contains a reasonable value.

Too many workers can harm automation due to CPU and Memory starvation.  Typically this value should not exceed 50% of the available CPU cores \(including hyper-threads if available\) and 2GB of RAM per Agent worker.

> For example, if the host has 8 logical processors \(cores\), it is recommended to not exceed 4 Agent workers.

The easiest way to set the maximum allowed workers amount is via the TestProject Application:

* Navigate to the _Agents_ screen
* Expand the line of the Agent you want to configure 
* Set the desired value into the `Max Workers` field

#### Environment Variable

Another option to configure the maximum allowed workers is by setting a value in the `TP_MAX_WORKERS` environment variable.

> Notes:
>
> * This configuration will override the configuration set via UI. 
> * Changes to the configuration take effect after Agent is fully **quit** and not only **restarted**.
> * If the configuration in the UI is updated, it will be in effect until Agent is restarted, after which, the local configuration will prevail again.

#### Local Configuration

Before an Agent is registered with your account, or when the internet connectivity is not available to retrieve the setting set via the TestProject Application, the same configuration can be set by changing the value of `maxWorkers` property in the `agent-configuration.json` file, available in Agent's data folder:

* Windows - `%appdata%\TestProject\Agent\agent-configuration.json`
* MacOS - `~/Library/Application Support/TestProject/Agent/agent-configuration.json`
* Linux - `./testproject/agent/agent-configuration.json`
* Docker - `/var/testproject/agent/agent-configuration.json`

> Notes:
>
> * This local configuration will override the configuration set via UI.
> * Changes to the configuration take effect after Agent is fully **quit** and not only **restarted**.
> * If the `TP_MAX_WORKERS` is set, it will override the configuration set via the `agent-configuration.json` file. 
> * If the configuration in the UI is updated, it will be in effect until Agent is restarted, after which, the local configuration will prevail again.

### Parallel Execution

Before the release of TestProject `3.0`, each Agent could run a single Test or a Job at a time.  When an additional Test or a Job was submitted, it was placed into a queue and sent to the Agent after the last reported that it's idle.

Since TestProject `3.0`, a single Agent can execute more than one Test or Job in parallel.  This can be either multiple tests on one or more browsers or devices, multiple _serial_ Jobs, or multiple _parallel_ Jobs.

> The execution might still become queued when the amount of active workers equals the maximum configured. It will be sent to the Agent when a worker will become available.

### Parallelization Options

Besides being able to run multiple Tests and Jobs in parallel, TestProject provides multiple parallelization options:

For "ad-hoc" tests execution:

* Targets - Browsers or Devices \(including virtual\)

For Jobs:

* Targets - Browsers or Devices \(including virtual\)
* Tests & Data-Driven Tests

#### Parallel Targets \(Browsers / Devices\)

The easiest way to enable parallel execution for targets \(browsers or devices\) is via the Job execution settings, selecting the `Parallel` execution option. The same is possible when executing a single test, by selecting the appropriate option in the Test Execution wizard.

**Parallel Targets - Example \#1**

A _web_ job and an Agent configured with two \(2\) maximum allowed workers:

* Browsers
  * Chrome
  * Firefox
* Tests
  * Test \#1 
  * Test \#2

Execution Summary:

1. Having the `Parallel` execution option **selected**, tests in this Job will be executed _in parallel on both_ the _Chrome_ and the _Firefox_ browsers:

```text
+-------------+ +-------------+
|             | |             |
|   Chrome    | |   Firefox   |
|             | |             |
+-------------+ +-------------+
+-------------+ +-------------+
|             | |             |
|   Test #1   | |   Test #1   |
|             | |             |
+-------------+ +-------------+
+-------------+ +-------------+
|             | |             |
|   Test #2   | |   Test #2   |
|             | |             |
+-------------+ +-------------+
```

**Parallel Targets - Example \#2**

A _web_ job and an Agent configured with two \(2\) maximum allowed workers:

* Browsers
  * Chrome
  * Firefox
  * Edge
* Tests
  * Test \#1 
  * Test \#2

Execution Summary:

1. Having the `Parallel` execution option **selected**, tests in this Job will be executed _in parallel on both_ the _Chrome_ and the _Firefox_ browsers
2. Since the maximum allowed workers are set to two \(**2**\), and there are three \(3\) target browsers configured for this job, the third one will start after one of the first two finishers.

**Total**: 3 executions, maximum 2 in parallel:

```text
+-------------+ +-------------+
|             | |             |
|   Chrome    | |   Firefox   |
|             | |             |
+-------------+ +-------------+
+-------------+ +-------------+
|             | |             |
|   Test #1   | |   Test #1   |
|             | |             |
+-------------+ +-------------+
+-------------+ +-------------+
|             | |             |
|   Test #2   | |   Test #2   |
|             | |             |
+-------------+ +-------------+

+-----------------------------+

+-------------+ 
|             | 
|    Edge     | 
|             | 
+-------------+ 
+-------------+ 
|             | 
|   Test #1   | 
|             | 
+-------------+ 
+-------------+ 
|             | 
|   Test #2   | 
|             | 
+-------------+
```

#### Parallel Web Tests

Besides executing targets in parallel, it is also possible to execute tests in parallel. This configuration can be also enabled via the Job configuration by selecting the `Run both browsers & tests in parallel` checkbox.

Parallel execution of tests assumes that there is no relation between the tests and they are **mutually independent**. Therefore if your tests in a job are organized in a specific order \(for example assuming a login sequence, before authenticated access actions\), enabling tests parallelization is not in your best interest as there is no guarantee for the tests execution order.

Also, note that enabling `Run both browsers & tests in parallel`, assumes:

* Tests will be executed in parallel on all configured targets.
* Tests with Data-Sources will be split into independent concurrent executions.

Review the following examples to better understand how it works:

**Parallel Tests - Example \#1**

A _web_ job and an Agent configured with two \(**2**\) maximum allowed workers:

* Browsers
  * Chrome
  * Firefox
* Tests
  * Test \#1 
  * Test \#2

Execution Summary:

1. Having the `Parallel` execution option **selected**, tests in this Job will be executed _in parallel_. 
2. When the `Run both browsers & tests in parallel` option is **selected**, the tests will be parallelized on all targets.

**Total**: 4 executions, maximum 2 in parallel:

```text
+-------------+ +-------------+
|             | |             |
|   Chrome    | |   Firefox   |
|             | |             |
+-------------+ +-------------+
+-------------+ +-------------+
|             | |             |
|   Test #1   | |   Test #1   |
|             | |             |
+-------------+ +-------------+

+-----------------------------+

+-------------+ +-------------+
|             | |             |
|   Chrome    | |   Firefox   |
|             | |             |
+-------------+ +-------------+
+-------------+ +-------------+
|             | |             |
|   Test #2   | |   Test #2   |
|             | |             |
+-------------+ +-------------+
```

**Parallel Tests - Example \#2**

A _web_ job and an Agent configured with two \(**2**\) maximum allowed workers:

* Browsers
  * Chrome
  * Firefox
* Tests
  * Test \#1 
  * Test \#2
  * Test \#3

Execution Summary:

1. Having the `Parallel` execution option **selected**, tests in this Job will be executed _in parallel_.
2. When the `Run both browsers & tests in parallel` option is **selected**, the tests will be parallelized on all targets.
3. Since the maximum allowed workers are set to two \(**2**\), only two execution will be concurrent.

**Total**: 6 executions, maximum 2 in parallel:

```text
+-------------+ +-------------+
|             | |             |
|   Chrome    | |   Firefox   |
|             | |             |
+-------------+ +-------------+
+-------------+ +-------------+
|             | |             |
|   Test #1   | |   Test #1   |
|             | |             |
+-------------+ +-------------+

+-----------------------------+

+-------------+ +-------------+
|             | |             |
|   Chrome    | |   Firefox   |
|             | |             |
+-------------+ +-------------+
+-------------+ +-------------+
|             | |             |
|   Test #2   | |   Test #2   |
|             | |             |
+-------------+ +-------------+

+-----------------------------+

+-------------+ +-------------+
|             | |             |
|   Chrome    | |   Firefox   |
|             | |             |
+-------------+ +-------------+
+-------------+ +-------------+
|             | |             |
|   Test #3   | |   Test #3   |
|             | |             |
+-------------+ +-------------+
```

**Parallel Tests - Example \#3**

A _web_ job and an Agent configured with five \(**5**\) maximum allowed workers:

* Browsers
  * Chrome
  * Firefox
* Tests
  * Test \#1 
  * Test \#2
  * Test \#3

Execution Summary:

1. Having the `Parallel` execution option **selected**, tests in this Job will be executed _in parallel_.
2. When the `Run both browsers & tests in parallel` option is **selected**, the tests will be parallelized on all targets.
3. Since the maximum allowed workers are set to five \(**5**\), only five \(5\) tests will be executed at a time.

**Total**: 6 executions, maximum 5 in parallel:

```text
+-------------+ +-------------+ +-------------+ +-------------+ +-------------+
|             | |             | |             | |             | |             |
|   Chrome    | |   Firefox   | |   Chrome    | |   Firefox   | |   Chrome    |
|             | |             | |             | |             | |             |
+-------------+ +-------------+ +-------------+ +-------------+ +-------------+
+-------------+ +-------------+ +-------------+ +-------------+ +-------------+
|             | |             | |             | |             | |             |
|  Test #1    | |  Test #1    | |  Test #2    | |  Test #2    | |  Test #3    |
|             | |             | |             | |             | |             |
+-------------+ +-------------+ +-------------+ +-------------+ +-------------+

+-----------------------------------------------------------------------------+

+-------------+ 
|             | 
|   Firefox   | 
|             | 
+-------------+ 
+-------------+ 
|             | 
|  Test #3    | 
|             | 
+-------------+
```

**Parallel Tests - Example \#4**

A _web_ job and an Agent configured with five \(**5**\) maximum allowed workers:

* Browsers
  * Chrome
  * Firefox
  * Edge
* Tests
  * Test \#1 
  * Test \#2
  * Test \#3

Execution Summary:

1. Having the `Parallel` execution option **selected**, tests in this Job will be executed _in parallel_.
2. When the `Run both browsers & tests in parallel` option is **selected**, the tests will be parallelized on all targets.
3. Since the maximum allowed workers are set to five \(**5**\), only five \(5\) tests will be executed at a time.

**Total**: 9 executions, maximum 5 in parallel:

```text
+-------------+ +-------------+ +-------------+ +-------------+ +-------------+
|             | |             | |             | |             | |             |
|   Chrome    | |   Firefox   | |    Edge     | |   Chrome    | |   Firefox   |
|             | |             | |             | |             | |             |
+-------------+ +-------------+ +-------------+ +-------------+ +-------------+
+-------------+ +-------------+ +-------------+ +-------------+ +-------------+
|             | |             | |             | |             | |             |
|  Test #1    | |  Test #1    | |  Test #1    | |  Test #2    | |  Test #2    |
|             | |             | |             | |             | |             |
+-------------+ +-------------+ +-------------+ +-------------+ +-------------+

+-----------------------------------------------------------------------------+

+-------------+ +-------------+ +-------------+ +-------------+
|             | |             | |             | |             |
|    Edge     | |   Chrome    | |   Firefox   | |    Edge     |
|             | |             | |             | |             |
+-------------+ +-------------+ +-------------+ +-------------+
+-------------+ +-------------+ +-------------+ +-------------+
|             | |             | |             | |             |
|  Test #2    | |  Test #3    | |  Test #3    | |  Test #3    |
|             | |             | |             | |             |
+-------------+ +-------------+ +-------------+ +-------------+
```

**Parallel Web Tests with Data-Sources**

In addition to the parallel execution of tests, having tests with data source configured, will execute the data-driven iterations in parallel as well. There is no need to enable this feature explicitly, selecting the `Run both browsers & tests in parallel` option assumes parallelization of their data-driven iterations.

The simplest example would be a test that verifies a login sequence with different credentials stored in a data source such as a CSV file. This verification can run independently, each execution with different credentials set and in parallel on multiple targets.

**Parallel Tests with Data-Source - Example \#1**

A _web_ job and an Agent configured with five \(**5**\) maximum allowed workers:

* Browsers
  * Chrome
* Tests
  * Test \#1 
    * Data-Source with ten \(10\) lines

Execution Summary:

1. Having the `Parallel` execution option **selected**, tests in this Job will be executed _in parallel_.
2. When the `Run both browsers & tests in parallel` option is **selected**, the tests will be parallelized on all targets.
3. Since the first test has 10 data-driven iterations, they will be parallelized on all targets.
4. Since the maximum allowed workers is set to five \(**5**\), only five \(5\) executions at a time will run in parallel.

**Total**: 10 executions, maximum 5 in parallel:

```text
+-------------+ +-------------+ +-------------+ +-------------+ +-------------+
|             | |             | |             | |             | |             |
|   Chrome    | |   Chrome    | |   Chrome    | |   Chrome    | |   Chrome    |
|             | |             | |             | |             | |             |
+-------------+ +-------------+ +-------------+ +-------------+ +-------------+
+-------------+ +-------------+ +-------------+ +-------------+ +-------------+
|             | |             | |             | |             | |             |
|  Test #1    | |  Test #1    | |  Test #1    | |  Test #1    | |  Test #1    |
|  Line #1    | |  Line #2    | |  Line #3    | |  Line #4    | |  Line #5    |
|             | |             | |             | |             | |             |
+-------------+ +-------------+ +-------------+ +-------------+ +-------------+

+-----------------------------------------------------------------------------+

+-------------+ +-------------+ +-------------+ +-------------+ +-------------+
|             | |             | |             | |             | |             |
|   Chrome    | |   Chrome    | |   Chrome    | |   Chrome    | |   Chrome    |
|             | |             | |             | |             | |             |
+-------------+ +-------------+ +-------------+ +-------------+ +-------------+
+-------------+ +-------------+ +-------------+ +-------------+ +-------------+
|             | |             | |             | |             | |             |
|  Test #1    | |  Test #1    | |  Test #1    | |  Test #1    | |  Test #1    |
|  Line #6    | |  Line #7    | |  Line #8    | |  Line #9    | |  Line #10   |
|             | |             | |             | |             | |             |
+-------------+ +-------------+ +-------------+ +-------------+ +-------------+
```

**Parallel Tests with Data-Source - Example \#2**

A _web_ job and an Agent configured with five \(**6**\) maximum allowed workers:

* Browsers
  * Chrome
  * Firefox
  * Edge
* Tests
  * Test \#1 
    * Data-Source with two \(2\) lines
  * Test \#2
  * Test \#3
    * Data-Source with two \(2\) lines

Execution Summary:

1. Having the `Parallel` execution option **selected**, tests in this Job will be executed _in parallel_.
2. When the `Run both browsers & tests in parallel` option is **selected**, the tests will be parallelized on all targets.
3. Since some tests have data-driven iterations, they will be parallelized on all targets.
4. Since the maximum allowed workers is set to five \(**6**\), only five \(6\) executions at a time will run in parallel.

**Total**: 15 executions, maximum 6 in parallel:

> Explanation:  Test \#1 has 2 iterations, Test \#2 has one, and Test \#3 has 2 iterations. In total it's 5 executions.  Since there are 3 browsers configured, 5 executions should run 3 times, making it **15** executions in total.

```text
+-------------+ +-------------+ +-------------+ +-------------+ +-------------+ +-------------+
|             | |             | |             | |             | |             | |             |
|   Chrome    | |   Firefox   | |    Edge     | |   Chrome    | |   Firefox   | |    Edge     |
|             | |             | |             | |             | |             | |             |
+-------------+ +-------------+ +-------------+ +-------------+ +-------------+ +-------------+
+-------------+ +-------------+ +-------------+ +-------------+ +-------------+ +-------------+
|             | |             | |             | |             | |             | |             |
|  Test #1    | |  Test #1    | |  Test #1    | |  Test #1    | |  Test #1    | |  Test #1    |
|  Line #1    | |  Line #1    | |  Line #1    | |  Line #2    | |  Line #2    | |  Line #2    |
|             | |             | |             | |             | |             | |             |
+-------------+ +-------------+ +-------------+ +-------------+ +-------------+ +-------------+

+---------------------------------------------------------------------------------------------+

+-------------+ +-------------+ +-------------+ +-------------+ +-------------+ +-------------+
|             | |             | |             | |             | |             | |             |
|   Chrome    | |   Firefox   | |    Edge     | |   Chrome    | |   Firefox   | |    Edge     |
|             | |             | |             | |             | |             | |             |
+-------------+ +-------------+ +-------------+ +-------------+ +-------------+ +-------------+
+-------------+ +-------------+ +-------------+ +-------------+ +-------------+ +-------------+
|             | |             | |             | |             | |             | |             |
|  Test #2    | |  Test #2    | |  Test #2    | |  Test #3    | |  Test #3    | |  Test #3    |
|             | |             | |             | |  Line #1    | |  Line #1    | |  Line #1    |
|             | |             | |             | |             | |             | |             |
+-------------+ +-------------+ +-------------+ +-------------+ +-------------+ +-------------+

+---------------------------------------------------------------------------------------------+

+-------------+ +-------------+ +-------------+
|             | |             | |             |
|   Chrome    | |   Firefox   | |    Edge     |
|             | |             | |             |
+-------------+ +-------------+ +-------------+
+-------------+ +-------------+ +-------------+
|             | |             | |             |
|  Test #3    | |  Test #3    | |  Test #3    |
|  Line #2    | |  Line #2    | |  Line #2    |
|             | |             | |             |
+-------------+ +-------------+ +-------------+
```

## Limitations

* Only one Safari browser instance can be active at any given time, and only one WebDriver session at a time can be attached to the browser instance. For more information, refer to [WebDriver for Safari](https://developer.apple.com/documentation/webkit/) documentation.
* Mobile device or emulator/simulator can not run more than one concurrent test at a time. Therefore to scale your mobile tests use multiple physical or virtual devices.
* Cloud providers such as SauceLabs or BrowserStack charge for concurrent execution sessions, before using their browsers or devices as targets, make sure that you have enough concurrent sessions allowed \(otherwise executions will be queued\) and run-time minutes.
* Virtual Agents can not run parallel executions, and their maximum workers setting is always one \(1\)

