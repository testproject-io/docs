# Using AI to Improve Testing

Artificial Intelligence is a much discussed topic. Some talk about AI as if it will replace testers, but here at TestProject we believe in the incredible value that testers can add to any project. We also believe that AI is a powerful tool that has come a long way in the last few years. In our goal to help testers become better at what they do, we have looked into ways that we can leverage this technology in our product so that we can help testers get even better at what they do. We use our AI to help out with a number of different things. Our AI driven technologies work for both web and mobile tests.

## Self Healing

One thing that many test automation teams have found is that test maintenance takes up a lot of time. Often tests will fail due to changing or moving locators. Humans can easily correct for this, but traditional test automation can't. This leads to a lot of time being spent on updating tests. This kind of work can be tedious and so TestProject has created self-healing capabilities. This AI-driven capability will identify one main way to identify an element, but will also find a number of other possible ways to locate the element. If something breaks such that the primary locator strategy does not work, it will automatically detect that it is broken and then use the fallback strategies to find the element for you.

This results in testers spending much less of their valuable time in debugging tests that unnecessarily fail. In turn, this frees up the testers to dig deeper into the application, find more important bugs, and add more valuable tests.

## Adaptive Wait

Another AI driven setting in TestProject is the adaptive wait functionality. With this technology, you won't need to worry about failed tests due to changes in page load times. You also don't need to worry about having tests that run much longer than then necesary to due to explicit waits programmed into them. You can learn more about how to us the adaptive wait technology in [this](../tips-and-tricks/explicit-wait-and-adaptive-wait.md) tips and tricks article.&#x20;

This technology automatically optimizing the wait times for different automation actions so that your tests are running as efficiently as possible while not failing due to unecessary time outs. When using this technology, you can trust your tests results without needing to build in long wait times between tests steps.

## Automation Assistant

In the spirit of having AI technology work with testers and not try to replace them, the TestProject automation assistant will give you suggestions that help make your tests more stable and valuable. If the self-healing technogoly correct a locator the automation assistant will let you know and offer you a suggestion for a new locator to use. It will also help stabilize your tests in the event of pop-ups or other page actions that can sometimes interfere with the running of UI tests.&#x20;

The automation assistant is on by default, but you can double check that you have not disabled it by going to the **Test** tab of the recorder.

![Automation Assistant](<../.gitbook/assets/image (407).png>)

In particular, if you have tests that were recorded with earlier versions of the recorder, and that are a bit flaky, you may want to check that this option is enabled.&#x20;

With the power of AI-driven, self-healing tests TestProject has made it possible to have tests that are easy to create, run, and maintain. Test flakyness is one of the leading challenges for UI automation and with the TestProject recorder you get powerful technology that deals with the problem for free! &#x20;
