# Behavior-driven development \(BDD\)

{% hint style="success" %}
**Behavior-driven development \(BDD\)** is an extension of test-driven development \(TDD\): development that makes use of a simple, domain-specific scripting language.
{% endhint %}

### Method names

Test method names should be sentences. You should read tests like this:

```text
CustomerLookup
- finds customer by id
- fails for duplicate customers
- ...
```

### Naming template

A simple sentence template keeps test methods focused. There is a convention of starting test method names with the word “_should_ ”. **The class** _**should**_ **do something** – means you can only define a test for the current class. This keeps you focused. If you find yourself writing a test whose name doesn’t fit this template, it suggests the behavior may belong elsewhere.

### “Behaviour” is a more useful word than “test”

That’s not to say that testing isn’t intrinsic to TDD – the resulting set of methods is an effective way of ensuring your code works. However, if the methods do not comprehensively describe the behaviour of your system, then they are lulling you into a false sense of security.

{% hint style="info" %}
**Requirements are behaviour, too.**
{% endhint %}

### Ubiquitous language

**Scenario** is the template that is loose enough that it wouldn’t feel artificial or constraining to analysts but structured enough that we could break the story into its constituent fragments and automate them.

> **Given** some initial context \(the givens\),  
> **When** an event occurs,  
> **Then** ensure some outcomes.

Example:

```text
Story: Returns go to stock

As a store owner
In order to keep track of stock
I want to add items back to stock when they're returned.

Scenario 1: Refunded items should be returned to stock
Given that a customer previously bought a black sweater from me
And I have three black sweaters in stock.
When they return the black sweater for a refund
Then I should have four black sweaters in stock.

Scenario 2: Replaced items should be returned to stock
Given that a customer previously bought a blue garment from me
And I have two blue garments in stock
And three black garments in stock.
When they return the blue garment for a replacement in black
Then I should have three blue garments in stock
And two black garments in stock.
```

### Acceptance criteria should be executable

The fragments of the scenario – the givens, event, and outcomes – are fine-grained enough to be represented directly in code.

For C\# you can use **SpecFlow** \(provides a syntax which allow non-programmers to define the behaviors which developers can then translate into automated tests\)**:**

{% code-tabs %}
{% code-tabs-item title="CalculatorSteps.cs" %}
```csharp
using System;
using TechTalk.SpecFlow;
using Microsoft.VisualStudio.TestTools.UnitTesting;
using Example;

namespace MyProject.Specs
{
    [Binding]
    public class CalculatorSteps
    {
        private int result; 
        private Calculator calculator = new Calculator();

        [Given(@"I have entered (.*) into the calculator")]
        public void GivenIHaveEnteredIntoTheCalculator(int number)
        {
            calculator.FirstNumber = number;
        }

        [Given(@"I have also entered (.*) into the calculator")]
        public void GivenIHaveAlsoEnteredIntoTheCalculator(int number)
        {
            calculator.SecondNumber = number;
        }

        [When(@"I press add")]
        public void WhenIPressAdd()
        {
            result = calculator.Add();
        }
        
        [Then(@"the result should be (.*) on the screen")]
        public void ThenTheResultShouldBeOnTheScreen(int expectedResult)
        {
            Assert.AreEqual(expectedResult, result);
        }
    }
}
```
{% endcode-tabs-item %}

{% code-tabs-item title="Calculator.feature" %}
```text
Feature: Calculator
       In order to avoid silly mistakes
       As a math idiot
       I want to be told the sum of two numbers

@mytag
Scenario: Add two numbers
       Given I have entered 50 into the calculator
       And I have also entered 70 into the calculator
       When I press add
       Then the result should be 120 on the screen
```
{% endcode-tabs-item %}
{% endcode-tabs %}

