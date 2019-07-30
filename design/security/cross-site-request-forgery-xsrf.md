# Cross-Site Request Forgery \(XSRF\)

{% hint style="success" %}
**Cross-site request forgery** \(also known as XSRF or CSRF\) is an attack against web-hosted apps whereby a malicious web app can influence the interaction between a client browser and a web app that trusts that browser.
{% endhint %}

These attacks are possible because web browsers send some types of authentication tokens automatically with every request to a website. This form of exploit is also known as a _one-click attack_ or _session riding_ because the attack takes advantage of the user's previously authenticated session.

### Example of a CSRF attack

* A user signs into `www.good-banking-site.com` using forms authentication.
* The user visits a malicious site, `www.bad-crook-site.com`. It contains such HTML:

```markup
<h1>Congratulations! You're a Winner!</h1>
<form action="http://good-banking-site.com/api/account" method="post">
    <input type="hidden" name="Transaction" value="withdraw">
    <input type="hidden" name="Amount" value="1000000">
    <input type="submit" value="Click to collect your prize!">
</form>
```

* The user selects the submit button. The browser makes the request and automatically includes the authentication cookie for the requested domain, `www.good-banking-site.com`.
* The request runs on the `www.good-banking-site.com` server with the user's authentication context and can perform any action that an authenticated user is allowed to perform.

In addition to the scenario where the user selects the button to submit the form, the malicious site could:

* Run a script that automatically submits the form.
* Send the form submission as an AJAX request.
* Hide the form using CSS.

{% hint style="info" %}
Using **HTTPS** doesn't prevent a CSRF attack. The malicious site can send an `https://www.good-banking-site.com/` request just as easily as it can send an insecure request.
{% endhint %}

Some attacks target endpoints that respond to GET requests, in which case an image tag can be used to perform the action. This form of attack is common on forum sites that permit images but block JavaScript.

{% hint style="danger" %}
**GET requests that change state are insecure. A best practice is to never change state on a GET request.**
{% endhint %}

###  <a id="aspnet-core-antiforgery-configuration"></a>

