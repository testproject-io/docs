---
description: >-
  This document will show you how to set up, and perform various actions on
  Google Sheets and Drive using TestProject Google Actions. This can be useful
  if you store test parameters with Google Sheets.
---

# Google Actions

## Set-Up

Google Authorization Process of using their API has two options, using an OAuth 2.0 token, or a JWT token from a Service Account.

By Choosing OAuth, one has direct access to his personal Google software like Drive, Sheets and so on, but using this method requires the **Browser to open to accept the token**, which is **NOT possible while automating**.

For automating, we can use a **JWT token** generated from a Google **Service Account**.

### Setting Up A Service Account

First, navigate to Google Developer Console, and choose the Google Account who should be the owner of the Service Account.

{% embed url="https://console.developers.google.com/" %}

![](<../../.gitbook/assets/image (300) (1).png>)



**Go to IAM  Admin**

![](<../../.gitbook/assets/image (317).png>)

![](<../../.gitbook/assets/image (332).png>)

If you do not have any Project in Google Developer Console, create one by navigating here

{% embed url="https://console.cloud.google.com/cloud-resource-manager" %}

Click on Create Project:

![](<../../.gitbook/assets/image (309).png>)

You can give it any name/location, it does not matter.

After you have your project, on the IAM & Admin page, make sure you are focused on that project.

![](<../../.gitbook/assets/image (304).png>)



Now go to the Service Accounts:

![](<../../.gitbook/assets/image (302).png>)

Create a new Service Account:



![](<../../.gitbook/assets/image (320).png>)

You can give it any Name and Description

![](<../../.gitbook/assets/image (305).png>)

And click on CREATE, for the Role, select Currently Used (Owner)

![](<../../.gitbook/assets/image (318).png>)



You can add additional people who can use this Service account for their needs here, or later.

![](<../../.gitbook/assets/image (299).png>)

Once everything is ready, click on DONE.

Next, we will generate the JWT token to use in the addon.

### Generate JWT Token

In the Service Account we just created, click on the 3 dots on the right, and click on Create Key:

![](<../../.gitbook/assets/image (311).png>)

Select JSON and Click CREATE

![](<../../.gitbook/assets/image (334).png>)





**Now it will generate the JWT token, and download it locally to your computer, save it somewhere safe as we will use it in ALL the actions of this addon for Authentication!**

Now we have the JWT token, we will input it as a **Secret Parameter** in TestProject to be encrypted inside the tests that use the Addon.

### Enter JWT Token In TestProject

In the test, we will go to Parameters:

![](<../../.gitbook/assets/image (298).png>)

Create a new Test/Project Parameter:

![](<../../.gitbook/assets/image (308).png>)

This parameter will hold the JWT token, we will make it a secret parameter, paste the contents of the JWT token that was generated inside this parameter:

![](<../../.gitbook/assets/image (294).png>)

And we will use that parameter inside the JsonSecrets input Field in every action.

### Set Up Google Drive With A Shared Account

Service Accounts are considered Virtual Machines, they have their own Google Sheets and Google Drive **(With no UI)**, so to access your personal items from another account, they need to be shared **(As well as be given access permissions in the Service Account as we saw above while creating the account).**

Enter the Desired Google Drive account, after that, create/select a Shared Drive:

![](<../../.gitbook/assets/image (301).png>)

If you do not have one. create a new Shared Drive:

![](<../../.gitbook/assets/image (319).png>)

After you have created the Shared Drive,  we will now give it permissions for the Service Account to use, Right-click on the Shared Drive and click on Manage Members:

![](<../../.gitbook/assets/image (323).png>)

Now we will add the email of the service account, go back to the[ **IAM & Admin**](https://console.developers.google.com/iam-admin/) **page, you will see your service account has an email:**

![](<../../.gitbook/assets/image (327).png>)

Copy that email, and paste it in the Shared Drive as a new member.

![](<../../.gitbook/assets/image (329).png>)

`Make sure you give it Content Manager rights so it will have the proper permissions.`

Now you can move every file you wish to give access to use Service account, and you will be able to operate on that file using the Addon.

## Available Actions

Some Actions like Google Sheets Actions or Action to work with files in Google Drive require specific IDs.

### Get File ID From Google Drive

There are two ways to get the File ID from Google Drive:

#### From The UI

Head over to Google Drive, right-click on the file you wish to interact with, and click on Get Link

![](<../../.gitbook/assets/image (310).png>)

Inside the Link, there will be the File ID.

![](<../../.gitbook/assets/image (316).png>)

#### Using the Get File ID Action

The addon provides an action that will return all links that correspond with a specific file name, each ID is separated by a new line.

![Then after you get the ID, you can use it inside a paramter for other actions](<../../.gitbook/assets/image (325).png>)

### Get Sheet ID From Google Drive

Like in File ID, it is the same process, in your Google Drive, right-click on the sheet, click on Get Link and copy the ID:

![](<../../.gitbook/assets/image (330).png>)

![You can save the the Sheet ID inside a parameter to re use it across test steps](<../../.gitbook/assets/image (322).png>)

You can also get the Sheet ID from the URL while working on the sheet itself:

![](<../../.gitbook/assets/image (326).png>)

{% hint style="info" %}
Note: The ID stays static no matter if the file name changes or moves, so it is a one-time operation per file/sheet.
{% endhint %}

### Google Drive Actions

All Actions Require JsonSecret parameter which is shown in the **Generate JWT Token** Section.

{% tabs %}
{% tab title="Delete File" %}
This Action provides the ability to Delete a file on Google Drive.

_**Inputs**_

FileId -> The File ID to delete.

The action will pass if the file was deleted successfully.

![](<../../.gitbook/assets/image (324).png>)
{% endtab %}

{% tab title="Download File" %}
This Action provides the ability to download a file from Google Drive to a local path.

_**Inputs**_

FilePath -> Local path to download the file to, for example: C:\Test\downloaded\_file.jpg

FileId -> The ID of the file.

![](<../../.gitbook/assets/image (307).png>)
{% endtab %}

{% tab title="Get File ID" %}
This Action provides the ability to Get all IDs of a file according to its file name.

_**Inputs**_

FileName -> The file name to get the ID from (Can be more than one)

_**Output**_

All the corresponding IDs, separated by a new line

![](<../../.gitbook/assets/image (314).png>)
{% endtab %}

{% tab title="List Files" %}
This Action provides the ability to list all files in all folders in Google Drive, including shared drives.

_**Output**_

A String of all files in all Drives, separated by a new line

![](<../../.gitbook/assets/image (303).png>)
{% endtab %}

{% tab title="Upload File" %}
This Action provides the ability to upload a file to Google Drive

_**inputs**_

FilePath -> Local path to the file, for example: C:\Test\text\_stuff.txt

FileName -> Provide the name to the file on Google Drive (Default is the same name as local file)

FileContent -> The content-type of the file, you can see the types [here](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics\_of\_HTTP/MIME\_types) (Default is all types \*/\*).

_**Output**_

The FileID of the just uploaded file, can be reused for future actions.

![](<../../.gitbook/assets/image (328).png>)
{% endtab %}
{% endtabs %}



### Google Sheets Actions

All Actions Require JsonSecret parameter which is shown in the **Generate JWT Token** Section.

All Actions Require SheetID parameter which is shown in the **Get Sheet ID** Section.

{% tabs %}
{% tab title="Read up to 10 values from a Row" %}
This action provides the ability to read up to 10 values from one given row.

**Inputs**

Row -> Row number (Starts from 1)

Range -> The column range to get values from, for example A:C to get Column A to C

**Outputs**

Up to ten outputs per cell according to the given range

![](<../../.gitbook/assets/image (312).png>)
{% endtab %}

{% tab title="Read Value in Column and Row" %}
This action provides the ability to read a value from a specific column and row

_**Inputs**_

Column -> The column letter, for example, A, B, E1, etc..

Row -> The row number, starts from 1.

_**Output**_

The value inside the given row and column

![](<../../.gitbook/assets/image (335).png>)
{% endtab %}

{% tab title="Read Value Using Header And Row" %}
This action provides the ability to read a value from a specific row and a header value if the column number is not known.

_**Inputs**_

HeaderValue -> The header value to use (headers are the values in the first row of the Sheet)

Row -> The row number, starts from 1.

SheetName -> The name of the sheet to work with (Default is Sheet1)

_**Output**_

The column number of the item, if it was found.

![](<../../.gitbook/assets/image (315).png>)
{% endtab %}

{% tab title="Update Row With Given Values" %}
This action provides the ability to update a specific row with given values, each value is separated by a new line, and will be inputted to the corresponding cell.

_**Inputs**_

Row -> The row to update, starts from 1.

StartColumn -> The column to start updating from, starts from 1.

EndColumn -> The column to end the updates, including the column itself.

Data -> The value to input in each cell, separated by a new line.

![](<../../.gitbook/assets/image (306).png>)
{% endtab %}

{% tab title="Update Value in Column and Row" %}
This action provides the ability to update a value in a specific cell.

_**Inputs**_

Column -> The column index, starts from 1.

Row -> The row index, starts from 1.

Value -> The value to update with.

![](<../../.gitbook/assets/image (321).png>)
{% endtab %}

{% tab title="Update value using Header and Row" %}
This action provides the ability to update a value from a specific row and a header value if the column number is not known.

_**Inputs**_

HeaderValue -> The header value to use (headers are the values in the first row of the Sheet)

Row -> The row number, starts from 1.

SheetName -> The name of the sheet to work with (Default is Sheet1).

Value -> The value to update with.

_**Output**_

The column number of the item, if it was found.

![](<../../.gitbook/assets/image (297).png>)
{% endtab %}
{% endtabs %}





