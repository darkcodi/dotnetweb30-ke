# Test Pyramid concept

The test pyramid is a way of thinking about different kinds of automated tests should be used to create a balanced portfolio. Its essential point is that you should have many more low-level UnitTests than high level BroadStackTests running through a GUI.

![](../../.gitbook/assets/image%20%2855%29.png)

Test pyramid consists of 3 types of tests:

* unit,
* integration,
* end-to-end.

{% hint style="success" %}
The **concept of pyramid** refers to the ratio in which these types of tests are usually presented in a test suite.
{% endhint %}

As unit tests run fast, it makes sense to have more of them as they give the quickest feedback. On the contrary, end-to-end tests are the minority because they take a lot of time to execute.

Tests residing in each level have a different value proposition. The higher the level, the more protection against regression errors and false positives you get. But you do that at the expense of the feedback speed. Similarly, the lower the level, the faster your tests run, but at the expense of coupling your tests to the details of the classes' structure.

{% hint style="info" %}
While the test pyramid is a good **guideline** in general, you need to take into account the specifics of your own project. You don't have to have end-to-end tests if you think that integration tests will provide enough protection for your code base. The ratio between the number of the tests of different types is also **not a strict rule**.

If your project is quite simple in terms of business rules, it might make sense to have just a few unit tests, and focus the most of your effort on integration testing because integration with database and other sub-systems in this case would be the most risky area.
{% endhint %}

