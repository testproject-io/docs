# How can I swipe to find an element in a mobile test? (Swipe and Find Element Addon)

In TestProject, we implemented a smart swipe action to get an element that is not in the current page and requires a swipe action to get to it.

The swipe actions are part of the [Swipe and Find Element addon](https://addons.testproject.io/swipe-and-find-element).\
This addon allows you to swipe in all directions (Up/Down/Left/Right) in a smart way. First, it searches the element in the current page. If it finds it, it will not swipe. However, if it doesn't find it, it will start to swipe in the defined direction.

#### Defining the action's parameters <a href="#defining-the-actions-parameters" id="defining-the-actions-parameters"></a>

Let's have a look at the **Swipe to element (vertically)** action:

**SwipeDirection -** Allows you to control the swipe direction: Up/Down/Left/Right

**BottomMarginPercent & TopMarginPercent -** Defining the area in which your "finger" will perform the swipe action. This image explains it better:

![](<../../.gitbook/assets/image (480).png>)

**MaxSwipes -** Defines the amount of swipes you want to perform in this step. For example, if you set it to 3 swipes, it will try to find the element for 3 swipes maximum. If the element will be found before that, it will stop the swipes actions.

**TimeoutMilliseconds -** This parameter defines the time frame for this action. For example, setting the timeout to 5000, will search the element for 5 seconds maximum. If the element isn't found after 5 seconds, it will fail the step.

#### Possible failure scenarios <a href="#possible-failure-scenarios" id="possible-failure-scenarios"></a>

The action can fail if:&#x20;

1. The **TimeoutMilliseconds** exceeded and the element was not found
2. The **MaxSwipes** is reached and the element was not found
3. The **BottomMarginPercent** or **TopMarginPercent** were set too low and it caused the swipe actions to be too fast and it passed the element
