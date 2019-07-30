# Test-driven development \(TDD\)

{% hint style="success" %}
**Test-driven development** \(**TDD**\) is a software development process that relies on the repetition of a very short development cycle: requirements are turned into very specific _test cases_, then the software is improved so that the tests pass.
{% endhint %}

### Test-driven development cycle

1. Add a test.
2. Run all tests and see if the new test fails.
3. Write the code.
4. Run tests.
5. Refactor code.

### Best practices

Tests SHOULD:

* have consistent test structure \(**AAA: Arrange, Act, Assert\)**;
* be independent;
* be quick.

Tests SHOULD NOT:

* depend on system state manipulated from previously executed tests;
* assert precise execution behavior timing or performance;
* inspect more than necessary \(such tests are called "all-knowing oracles"\);
* test implementation details.

### Inside Out vs Outside In approaches

#### Inside Out TDD \(Bottom Up/Chicago School/Classic Approach\)

**Inside Out** TDD allows the developer to focus on one thing at a time. Each entity \(i.e. an individual module or single class\) is created until the whole application is built up.

In one sense the individual entities could be deemed worthless until they are working together, and wiring the system together at a late stage may constitute higher risk. On the other hand, focusing on one entity at a time helps parallelize development work within a team.

Full understanding of the system design is not required at the beginning. Only one entity needs to be identified to get started.

#### Outside In TDD \(Top Down/London School/Mockist Approach\)

**Outside In** TDD lends itself well to having a definable route through the system from the very start, even if some parts are initially hardcoded.

The tests are based upon user-requested scenarios, and entities are wired together from the beginning. This allows a fluent API to emerge and integration is proved from the start of development.

By focusing on a complete flow through the system from the start, knowledge of how different parts of the system interact with each other is required. As entities emerge, they are mocked or stubbed out, which allows their detail to be deferred until later.

