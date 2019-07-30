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

