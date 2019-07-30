# Test Organization patterns

## Named Test suite

We define a test suite, suitably named, that contains a set of tests that we wish to be able to run as a group.

![](../../.gitbook/assets/image%20%28153%29.png)

For each group of related tests that we would like to be able to run as a group, we can define a special Test Suite Factory with an Intent-Revealing Name. The Factory Method \[GOF\] can use any of several test suite construction techniques to return a Test Suite Object containing only the specific Testcase Objects we wish to execute.

## Test Case structure

### Testcase class per Class

We put all the Test Methods for one SUT class onto a single Testcase Class.

![](../../.gitbook/assets/image%20%2862%29.png)

We create a separate Testcase Class for each class we wish to test. Each Testcase Class acts as a home to all the Test Methods that are used to verify the behavior of the SUT class.

### Testcase class per Fixture

We organize Test Methods into Testcase Classes based on commonality of the test fixture.

![](../../.gitbook/assets/image%20%2832%29.png)

**Test fixture** is all the things we need to have in place in order to run a test and expect a particular outcome.

### Testcase class per Feature

We group the Test Methods onto Testcase Classes based on which testable feature of the SUT they exercise.

![](../../.gitbook/assets/image%20%28103%29.png)

We group our Test Methods onto Testcase Classes based on which feature of the Testcase Class they verify. This organizational scheme allows us to have smaller Testcase Classes and to see at a glance all the test conditions for a particular feature of the class

## Test Code Reuse

#### Test Utility method

We encapsulate the test logic we want to reuse behind a suitably named utility method.

![](../../.gitbook/assets/image%20%2837%29.png)

* **Creation Method** Creation Methods are used to create ready-to-use objects as part of fi xture setup. They hide the complexity of object creation and interdependencies from the test.
* **Custom assertion** Custom Assertions are used to specify test-specifi c equality in a way that is reusable across many tests. They hide the complexity of comparing the expected outcome with the actual outcome. Custom Assertions are typically free of side effects in that they do not interact with the SUT to retrieve the outcome; that task is left to the caller.

## Parameterized Test

We pass the information needed to do fi xture setup and result verification to a utility method that implements the entire test life cycle.

![](../../.gitbook/assets/image%20%28145%29.png)

The solution is to factor out the common logic into a utility method. When this logic includes all four parts of the entire Four-Phase Test life cycle—that is, fi xture setup, exercise SUT, result verification, and fixture teardown—we call the resulting utility method a Parameterized Test. This kind of test gives us the best coverage with the least code to maintain and makes it very easy to add more tests as they are needed.

## Location

#### Testcase superclass

We inherit reusable test-specific logic from an abstract Testcase Super class.

![](../../.gitbook/assets/image%20%288%29.png)

#### Test Helper

We define a helper class to hold any Test Utility Methods we want to reuse in several tests.

![](../../.gitbook/assets/image%20%2889%29.png)

In each test that wishes to use Test Helper's logic, we access the logic either using static method calls or via an instance created specifi cally for the purpose.

