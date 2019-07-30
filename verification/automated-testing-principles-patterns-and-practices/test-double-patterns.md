# Test double patterns

**Test Double:** How can we verify logic independently when code it depends on is unusable? How can we avoid Slow Tests?   
****We replace a component on which the SUT depends with a “test-specifi c equivalent.”

## Test Stub

We replace a real object with a test-specifi c object that feeds the desired indirect inputs into the system under test.

![](../../.gitbook/assets/image%20%2829%29.png)

## Test Spy

We use a Test Double to capture the indirect output calls made to another component by the SUT for later verification by the test.

![](../../.gitbook/assets/image%20%28159%29.png)

## Mock Object

We replace an object on which the SUT depends on with a test-specifi c object that verifi es it is being used correctly by the SUT

![](../../.gitbook/assets/image%20%2859%29.png)

## Fake Object

We replace a component that the SUT depends on with a much lighter-weight implementation.

![](../../.gitbook/assets/image%20%28125%29.png)

## Configurable Test Double

We confi gure a reusable Test Double with the values to be returned or verifi ed during the fi xture setup phase of a test.

![](../../.gitbook/assets/image%20%2828%29.png)

## Hard-coded Test Double

We build the Test Double by hard-coding the return values and/or expected calls.

![](../../.gitbook/assets/image%20%28140%29.png)

