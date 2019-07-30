# Test smells and how to avoid

## Conditional test logic

#### **Symptoms**

Conditional statements in the test \(if, switch\). Test code executes differently each time we run it.

#### **Possible solution**

We can replace the if statements that steer execution to a call to fail with a Guard Assertion \(Xunit\) that causes the test to fail before we reach the code we don’t want to execute. 

We can replace Conditional Test Logic for verification of complex objects with an Equality Assertion on an Expected Object. If the production code’s equals method is too strict, we can use a Custom Assertion  to defi ne test-specific equality.

## Hard-to-test code

#### **Symptoms**

Some kinds of code are inherently difficult to test—GUI components, multithreaded code, and test code, for example. It may be difficult to get at the code to be tested because it is not visible to a test. It may be problematic to compile a test because the code is too highly coupled to other classes.

#### **Possible solution**

The key to testing overly coupled code is to break the coupling \(a Test Double or, more specifically, a Test Stub or Mock Object\).

The key to testing asynchronous code is to separate the logic from the asynchronous access mechanism.

## Test code duplication

#### **Symptoms**

The same test code is repeated many times.

#### **Possible solution**

The best solution is to use an Extract Method refactoring to create a Test Utility Method from one of the examples and then to generalize that method to handle each of the copies.

## Test logic in production

#### **Symptoms**

The code that is put into production contains logic that should be exercised only during tests.

The logic in the SUT\(System Under Testing\) is there solely to support testing. This logic may be “extra stuff” that the tests require to gain access to the SUT’s internal state for fi xture setup or result verifi cation purposes. It may also consist of changes that the logic of the system undergoes when it detects that it is being tested.

#### **Possible solution**

Instead of adding test logic into the production code directly, we can move logic into a substitutable dependency. We can put code that should be run in only production into a Strategy \[GOF\] object that is installed by default and replaced by a Null Object when running our tests.

When a test requires test-specific equality, we should use a Custom Assertion instead of modifying the equals method**.**

## Obscure tests

#### **Symptoms**

We are having trouble understanding what behavior a test is verifying.

#### **Possible solution**

Use meaningfull namings, use Parameterized Creation Methods to get test objects, fixture values that do not matter to the test should be defaulted within Creation Methods. 

## Erratic tests

#### **Symptoms**

We have one or more tests that run but give different results depending on when they are run and who is running them.

#### **Possible solution**

 

![](../../.gitbook/assets/image%20%2867%29.png)

In case of Interacting Tests we could eliminate this problem entirely by using a Fresh Fixture \(each test constructs its own brand-new test fixture for its own private use\).

In case of Resource Leakage we should convert the test to use a Fresh Fixture by creating the resource as part of the test’s fixture setup phase. This approach ensures that the resource exists wherever it is run.

## Slow Tests

#### **Symptoms**

The tests take long enough to run that developers don’t run them every time they make a change to the SUT.

#### **Possible solution**

We can make our tests run much faster by replacing the slow components with a Test Double that provides near-instantaneous responses.

Reduce the amount of fi xture setup performed by each test.

Avoid asynchronicity in tests by testing the logic synchronously

## Assertion Roulette

#### **Symptoms**

It is hard to tell which of several assertions within the same test method caused a test failure.

#### **Possible solution**

Break up the test into a suite of Single-Condition Tests.

## Frequent Debugging

#### **Symptoms**

Manual debugging is required to determine the cause of most test failures.

#### **Possible solution**

Doing true test-driven development is the best way to avoid the circumstances that lead to Frequent Debugging**.** We should start as close as possible to the skin of the application and do storytest-driven development—that is, we should write unit tests for individual classes as well as component tests for the collections of related classes to ensure we have good Defect Localization.

## Fragile Tests

#### **Symptoms**

A test fails to compile or run when the SUT is changed in ways that do not affect the part the test is exercising.

#### **Possible solution**

![](../../.gitbook/assets/image%20%28160%29.png)

_Interface sensitivity_: define of a Higher-Level Language that is used to express the tests. The verbs in the test language are translated into the appropriate method calls by the encapsulation layer, which is then the only software that needs to be modifi ed when the interface is altered in somewhat backward-compatible ways.

_Behavioral sencitivity_: newly incorrect assumptions about the behavior of the SUT used during fixture setup may be encapsulated behind Creation Methods. Similarly, assumptions about the details of post-test state of the SUT can be encapsulated in Custom Assertions or Verifi cation Methods.

The best solution to _Data Sensitivity_ is to make the tests independent of the existing contents of the database—that is, to use a Fresh Fixture.

_Context sencitivity_: we need to control all the inputs of the SUT if our tests are to be deterministic. If we depend on inputs from other systems, we may need to control these inputs by using a Test Stub.

