# Test Suite

{% hint style="success" %}
A **test suite** \(validation suite\) is a collection of test cases that are intended to be used to test a software program to show that it has some specified set of behaviours.
{% endhint %}

A test suite often contains detailed instructions or goals for each collection of test cases and information on the system configuration to be used during testing. A group of test cases may also contain prerequisite states or steps, and descriptions of the following tests.

### **Types**

Occasionally, test suites are used to group similar test cases together. A system might have a smoke test suite that consists only of smoke tests or a test suite for some specific functionality in the system. It may also contain all tests and signify if a test should be used as a smoke test or for some specific functionality.

In model-based testing, one distinguishes between abstract test suites, which are collections of abstract test cases derived from a high-level model of the system under test, and executable test suites, which are derived from abstract test suites by providing the concrete, lower-level details needed to execute this suite by a program. An abstract test suite cannot be directly used on the actual system under test \(SUT\) because abstract test cases remain at a high abstraction level and lack concrete details about the SUT and its environment. An executable test suite works on a sufficiently detailed level to correctly communicate with the SUT and a test harness is usually present to interface the executable test suite with the SUT.

A test suite for a primality testing subroutine might consist of a list of numbers and their primality \(prime or composite\), along with a testing subroutine. The testing subroutine would supply each number in the list to the primality tester, and verify that the result of each test is correct.

