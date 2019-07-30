# Protecting against SQL-injection attacks

{% hint style="success" %}
A successful **SQL injection attack** enables a malicious user to execute commands in your application's database by using the privileges granted to your application's login.
{% endhint %}

Common vulnerabilities that make your data access code susceptible to SQL injection attacks include:

* Weak input validation.
* Dynamic construction of SQL statements without the use of type-safe parameters.
* Use of over-privileged database logins.

