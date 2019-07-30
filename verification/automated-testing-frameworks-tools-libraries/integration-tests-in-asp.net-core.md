# Integration tests in ASP.NET Core

Integration tests ensure that an app's components function correctly at a level that includes the app's supporting infrastructure, such as the database, file system, and network. ASP.NET Core supports integration tests using a unit test framework with a test web host and an in-memory test server.

### Introduction to integration tests

Integration tests evaluate an app's components on a broader level than unit tests. Unit tests are used to test isolated software components, such as individual class methods. Integration tests confirm that two or more app components work together to produce an expected result, possibly including every component required to fully process a request.

These broader tests are used to test the app's infrastructure and whole framework, often including the following components:

* Database
* File system
* Network appliances
* Request-response pipeline

Unit tests use fabricated components, known as fakes or mock objects, in place of infrastructure components. In contrast to unit tests, integration tests:

* Use the actual components that the app uses in production.
* Require more code and data processing.
* Take longer to run.

Therefore, limit the use of integration tests to the most important infrastructure scenarios. If a behavior can be tested using either a unit test or an integration test, choose the unit test.

{% hint style="warning" %}
Don't write integration tests for every possible permutation of data and file access with databases and file systems. Regardless of how many places across an app interact with databases and file systems, a focused set of read, write, update, and delete integration tests are usually capable of adequately testing database and file system components. Use unit tests for routine tests of method logic that interact with these components. In unit tests, the use of infrastructure fakes/mocks result in faster test execution.
{% endhint %}

{% hint style="info" %}
In discussions of integration tests, the tested project is frequently called the system under test, or "SUT" for short.
{% endhint %}

### ASP.NET Core integration tests

Integration tests in ASP.NET Core require the following:

* A test project is used to contain and execute the tests. The test project has a reference to the tested ASP.NET Core project, called the _system under test_ \(SUT\). _"SUT" is used throughout this topic to refer to the tested app._
* The test project creates a test web host for the SUT and uses a test server client to handle requests and responses to the SUT.
* A test runner is used to execute the tests and report the test results.

Integration tests follow a sequence of events that include the usual Arrange, Act, and Assert test steps:

1. The SUT's web host is configured.
2. A test server client is created to submit requests to the app.
3. The _Arrange_ test step is executed: The test app prepares a request.
4. The _Act_ test step is executed: The client submits the request and receives the response.
5. The _Assert_ test step is executed: The _actual_ response is validated as a _pass_ or _fail_ based on an _expected_ response.
6. The process continues until all of the tests are executed.
7. The test results are reported.

Usually, the test web host is configured differently than the app's normal web host for the test runs. For example, a different database or different app settings might be used for the tests.

Infrastructure components, such as the test web host and in-memory test server \([TestServer](https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.testhost.testserver?view=aspnetcore-2.2)\), are provided or managed by the `Microsoft.AspNetCore.Mvc.Testing` package. Use of this package streamlines test creation and execution.

The `Microsoft.AspNetCore.Mvc.Testing` package handles the following tasks:

* Copies the dependencies file \(_\*.deps_\) from the SUT into the test project's _bin_ directory.
* Sets the content root to the SUT's project root so that static files and pages/views are found when the tests are executed.
* Provides the [WebApplicationFactory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.mvc.testing.webapplicationfactory-1) class to streamline bootstrapping the SUT with `TestServer`.

The unit tests documentation describes how to set up a test project and test runner, along with detailed instructions on how to run tests and recommendations for how to name tests and test classes.

{% hint style="info" %}
When creating a test project for an app, separate the unit tests from the integration tests into different projects. This helps ensure that infrastructure testing components aren't accidentally included in the unit tests. Separation of unit and integration tests also allows control over which set of tests are run.
{% endhint %}

