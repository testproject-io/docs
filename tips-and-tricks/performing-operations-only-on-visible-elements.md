# Performing Operations only on Visible Elements

Sometimes when you are interacting with a page and trying to simulate realistic user interactions you will want to limit your interactions to only visible element. For example, imagine you were working on a page that had a dialogue popup that needed input before you could proceed. An automated test might still be able to interact with elements on the page that underlies that dialogue or pop-up, but actual human users could not do so. If you wanted to be able to more accurately simulate the user interactions on that page you would want to make sure that you couldn't click on or interact with those elements until the dialogue had been dismissed.

## Visible Elements Operations Addon

This is where the Visible Elements Operations addon can be helpful. This addon provides a number of actions like clicking on, typing text in, or clearing the contents of an element. It also has a number of actions that can verify different aspects of an element's state. Most of these actions are already built directly into the core TestProject tool, but this addon creates an additional constraint on these actions. They will only be executed if the element they are executed on is visible at the time.&#x20;

As with any addon in TestProject, using it is as easy as a [_1-click installation_](../testproject-addons/installing-community-addons-from-the-store.md)_ _and all the actions from this addon will immediately be available for you to use in your tests.&#x20;

![Install Visible Elements Operations Addon](<../.gitbook/assets/image (106).png>)
