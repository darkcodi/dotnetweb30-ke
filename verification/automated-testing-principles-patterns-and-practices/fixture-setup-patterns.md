# Fixture setup patterns

## Fresh Fixture

### Inline setup

Each Test Method creates its own Fresh Fixture by calling the appropriate constructor methods to build exactly the test fixture it requires.

![](../../.gitbook/assets/image%20%2830%29.png)

To execute an automated test, we require a text fixture that is well understood and completely deterministic. We can use the Fresh Fixture approach to build a Minimal Fixture for the use of this one test. Setting up the test fixture on an in-line basis in each test is the most obvious way to build it.

### Delegated setup

Each Test Method creates its own Fresh Fixture by calling Creation Methods from within the Test Methods.

![](../../.gitbook/assets/image%20%28147%29.png)

### Implicit setup

We build the test fixture common to several tests in the setUp method.

![](../../.gitbook/assets/image%20%28148%29.png)

## Shared Fixture

### Prebuilt fixture

We build the Shared Fixture separately from running the tests.

![](../../.gitbook/assets/image%20%2870%29.png)

### Lazy setup

We use Lazy Initialization of the fi xture to create it in the fi rst test that needs it.

![](../../.gitbook/assets/image%20%28163%29.png)

### SuiteFixture setup

We build/destroy the shared fi xture in special methods called by the Test Automation Framework before/after the fi rst/last Test Method is called.

![](../../.gitbook/assets/image%20%2898%29.png)

### Setup Decorator

We wrap the test suite with a Decorator that sets up the shared test fixture before running the tests and tears it down after all tests are done.

![](../../.gitbook/assets/image%20%2875%29.png)

### Chained tests

We let the other tests in a test suite set up the test fixture.

![](../../.gitbook/assets/image%20%2887%29.png)

Chained Tests offer a way to reuse the test fixture left over from one test and the Shared Fixture of a subsequent test.

