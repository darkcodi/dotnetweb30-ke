# Continuous testing

{% hint style="success" %}
**Continuous testing** was originally proposed as a way of reducing waiting time for feedback to developers by introducing development environment-triggered tests as well as more traditional developer/tester-triggered tests.
{% endhint %}

Continuous testing is the process of executing **automated tests** as part of the software delivery pipeline to obtain immediate feedback on the business risks associated with a software release candidate.

Continuous testing includes the validation of both **functional requirements** and **non-functional requirements**.

Tests are executed during or alongside **continuous integration \(CI\) — at least daily**.

For teams practicing **continuous delivery \(CD\)**, tests are commonly executed many times a day, **every time** that the application is updated **in the version control system**.

### Continuous testing vs automated testing

The goal of Continuous Testing is to apply "extreme automation" to stable, production-like test environments. Automation is essential for Continuous Testing. But automated testing is not the same as Continuous Testing.

**Automated testing** involves automated, **CI-driven execution** of whatever set of tests the team has accumulated.

**Continuous testing** involves executing a set of tests that is specifically designed to assess the **business risks** associated with a release candidate.

{% hint style="info" %}
With **automated testing**, a test failure may indicate **anything** from a critical issue to a violation of a trivial naming standard.

With **continuous testing**, a test failure always indicates a **critical business risk**.
{% endhint %}

