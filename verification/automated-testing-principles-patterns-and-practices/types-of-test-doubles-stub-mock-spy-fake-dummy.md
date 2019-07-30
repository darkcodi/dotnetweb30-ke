# Types of test doubles \(Stub, Mock, Spy, Fake, Dummy\)

There are at least five types of Test Doubles:

* **Test stub.** Used for providing the tested code with "indirect input".
* **Mock object.** Used for verifying "indirect output" of the tested code, by first defining the expectations before the tested code is executed.
* **Test spy.** Used for verifying "indirect output" of the tested code, by asserting the expectations afterwards, without having defined the expectations before the tested code is executed. It helps in recording information about the indirect object created.
* **Fake object.** Used as a simpler implementation, e.g. using an in-memory database in the tests instead of doing real database access.
* **Dummy object.** Used when a parameter is needed for the tested method but without actually needing to use the parameter.

For both manual and automated black box testing of service oriented architecture systems or microservices software developers and testers use test doubles that communicate with the system under test over a network protocol. These test doubles are called different names depending on the tool vendor. A commonly used term is service virtualization. Other names used include API simulation, API mock, HTTP stub, HTTP mock, over the wire test double.

Another form of test double is the Verified Fake, a Fake object whose behavior has been verified to match that of the real object using a set of tests that run against both the Verified Fake and the real implementation.

While there is no open standard for test double and the various types, there is momentum for continued use of these terms in this manner. Martin Fowler used these terms in his article, Mocks Aren't Stubs referring to Meszaros' book. Microsoft also used the same terms and definitions in an article titled, Exploring The Continuum Of Test Doubles.

