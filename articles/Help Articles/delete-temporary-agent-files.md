# Delete temporary agent files

Sometimes as part of fixing common errors, you will be requested to delete agent temporary files, this article described where to find them and how to delete them.

In order to perform the clean-up follow these steps.

#### 1) Quit the TestProject Agent <a href="#h_e9de0d5dad" id="h_e9de0d5dad"></a>

#### 2) Navigate to: <a href="#h_8cf9affe95" id="h_8cf9affe95"></a>

**Windows**

Open the `Start` menu, type `%appdata%\TestProject\Agent\` and hit enter.

**macOS**\
﻿Open `Files Finder` and choose `Go` form the top menu, select `Go to Folder` and type:\
﻿ `~/Library/Application Support/TestProject/Agent`

**Linux**\
﻿Navigate to `~/.testproject/agent/`\
﻿

#### 3) Clean these folders: <a href="#h_829f24b6e6" id="h_829f24b6e6"></a>

* `coded-tests`
* ﻿`data-sources`
* `addons`
* `apps`
* `executions`
* `logs`
* `temp`
* `workers-executions`

#### 4) Delete the following file: <a href="#h_5079b236c0" id="h_5079b236c0"></a>

* `lock`

**5) Start the TestProject Agent**

\
