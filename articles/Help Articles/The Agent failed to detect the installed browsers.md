# The Agent failed to detect the installed browsers

In some cases, the Agent can't detect any browsers or only a specific one.&#x20;

The agent should detect all the installed browsers on the machine that it's installed on. However, If one or more browsers are not detected, try these possible solutions:

#### For Windows Operating System <a href="#for-windows-operating-system" id="for-windows-operating-system"></a>

1. Make sure that the browser is indeed installed on your machine.
2. Open: **Start** → **Run** → **regedit** → **OK**.\
   Click on: **HKEY\_LOCAL\_MACHINE** → **SOFTWARE** → **Clients** → **StartMenuInternet** → You should see the missing browser there. If it's not there, it means that this browser is not installed on your machine. In that case, please install it and try again.\
   \
   You can also check in this location if you couldn't find it in the above: **HKEY\_LOCAL\_MACHINE** → **SOFTWARE** → **WOW6432Node** → **Clients** → **StartMenuInternet** → You should see the missing browser there. If it's not there, it means that this browser is not installed on the user's machine.
3. If none of the above solutions helped, try to reinstall the browser.&#x20;

#### For OS X Operating System <a href="#for-os-x-operating-system" id="for-os-x-operating-system"></a>

1. Make sure that the browser is indeed installed on your machine.
2. Open the **"System Information"** app, and check if you see the browsers (at least Chrome) in the Applications section. Then, restart the Agent and check if the browsers appear.\
   It should restart some macOS service that returns empty results to the Agent.
