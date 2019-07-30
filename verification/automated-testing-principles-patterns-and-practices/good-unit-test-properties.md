# Good unit test properties

### 1. A basic unit test: <a id="1abasicunittest"></a>

* does not depend on the environment; e.g. it will run on your computer and it will run on your colleague’s computer
* does not depend on other unit tests
* does not depend on external data
* does not have side effects

### 2. A good unit test: <a id="2agoodunittest"></a>

* asserts the results of your code
* tests a single unit of work \(mostly a method\)
* Covers all the paths of the code you want to test

### 3. A better unit test: <a id="3abetterunittest"></a>

* tests and asserts edge cases and different ranges of data
* runs fast \(&lt; 100ms\)
* is well-factored
    
## A unit test should have the following properties:
* It should be automated and repeatable.
* It should be easy to implement.
* It should be relevant tomorrow.
* Anyone should be able to run it at the push of a button.
* It should run quickly.
* It should be consistent in its results (it always returns the same result if you
don’t change anything between runs).
* It should have full control of the unit under test.
* It should be fully isolated (runs independently of other tests).
* When it fails, it should be easy to detect what was expected and determine how
to pinpoint the problem.
