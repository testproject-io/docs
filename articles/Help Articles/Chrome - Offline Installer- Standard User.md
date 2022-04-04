---
description: Chrome installed using offline installer is not detected
---

# Chrome - Offline Installer - Standard User

When using an offline installer for Google Chrome, it is installed to AppData folder instead of Program Files.

The good thing about installing Chrome in AppData folder is it doesn’t require UAC elevation so any user including Guest account will be able to successfully install without problems.

However, when launching TestProject Agent using another user (e.g. Administrator account) Chrome is not detected, because it's not installed for this user, nor in it's regular location under Program Files folder so that any user can access it.

To resolve this, either log in to the Administrator account and install Chrome using offline installer under this account or use the online installer which will install Google Chrome into Program Files folder for all users.
