---
description: >-
  In this article i will explain how to install and register the TestProject
  agent on LINUX based servers.
---

# Installing and registering the agent on LINUX servers

Installing an agent on a server is very useful. the agent will be avaiable to all users on the account, which can easely run thier test on it.\
I used an ubuntu server, running on VMware virtual machine for this example.

First thing you need to do is go to a machine with UI, and download the linux version of the agent from [here](https://app.testproject.io/#/download), click on downloadd for another platform, and choose Linux.\
Now copy the **“TestProjectAgent\_x64.sh”** file to the headless machine via network or VM mapped folder. I will show how to use VMware mapped folder here, but other VM options might be different.

Select your machine and go to the Edit option:\


![](<../../.gitbook/assets/image (561) (1).png>)

Then navigate to the options tab, choose shared folders, click add and add your path:

![](<../../.gitbook/assets/image (565).png>)

Click OK and run your machine.\
Run the command&#x20;

```shell
sudo vmhgfs-fuse .host:/ /mnt/ -o allow_other -o uid=1000
```

You will be asked for your password, insert it and continue.\
Now type: cd /mnt/\
Now type: ls\
You should see your folder, now enter this folder using: cd FOLDER\_NAME/\
Now type ls again, you should see the files inside.\
Go to the folder which houses **TestProjectAgent\_YOUR\_VERSION.sh** file, and run the command:

```shell
chmod +x TestProject_Agent_YOUR_VERSION.sh
```

Now run: ./TestProject\_Agent\_YOUR\_VERSION.sh

And follow the instructions given:\


![](<../../.gitbook/assets/image (518).png>)

At the end it will ask you if you want to start the application, type y and enter.\
Type the command: sudo apt install net-tools\
Type ifconfig\
Save the number shown after inet, this is the agents IP, you will use it to remotely register your agent on Linux server.\
Now open TestProject application with chrome browser, go to the agent tab and click Register agent: (you can browse to TestProject application from any desktop that have a browser as long as it on the same network as your Linux server)&#x20;

![](<../../.gitbook/assets/image (512).png>)

Type in the agent's IP saved from earlier, and choose a name for your agent:

![](<../../.gitbook/assets/image (488) (1).png>)

Click save, then register:\


![](<../../.gitbook/assets/image (543) (1).png>)

Congratulations! you have registered your Agent! it will now show in your agent tab:\


![](<../../.gitbook/assets/image (529).png>)

And is available for use!\
To run the agent once you restart the server:

run the `TestProjectAgent` command from the `testproject/agent` folder

![](<../../.gitbook/assets/image (449).png>)

And the agent will start.
