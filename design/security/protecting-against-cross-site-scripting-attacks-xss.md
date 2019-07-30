# Protecting against cross-site scripting attacks \(XSS\)

{% hint style="success" %}
**Cross-Site Scripting \(XSS\)** is a security vulnerability which enables an attacker to place client side scripts \(usually JavaScript\) into web pages.
{% endhint %}

When other users load affected pages the attacker's scripts will run, enabling the attacker to steal cookies and session tokens, change the contents of the web page through DOM manipulation or redirect the browser to another page.

XSS vulnerabilities generally occur when an application takes user input and outputs it to a page without validating, encoding or escaping it.

### Protecting your application against XSS <a id="protecting-your-application-against-xss"></a>

1. **Never put untrusted data into your HTML input**, unless you follow the rest of the steps below.
2. Before putting untrusted data inside an HTML element/attribute **ensure it's HTML encoded**. HTML encoding takes characters such as `<` and changes them into a safe form like `&lt`
3. Before putting untrusted data into JavaScript **ensure it's JavaScript encoded**. JavaScript encoding takes dangerous characters for JavaScript and replaces them with their hex, for example `<` would be encoded as `\u003C`

{% hint style="info" %}
The Razor engine used in MVC **automatically encodes** all output sourced from variables, unless you work really hard to prevent it doing so.
{% endhint %}

### Example:

```aspnet
@{
   var untrustedInput = "<\"123\">";
}

<div
   id="injectedData"
   data-untrustedinput="@untrustedInput" />
```

This will produce the following HTML:

```aspnet
<div
   id="injectedData"
   data-untrustedinput="&lt;&quot;123&quot;&gt;" />
```

