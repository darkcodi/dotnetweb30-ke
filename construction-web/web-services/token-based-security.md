# Token based security

### TOKEN BASED AUTHENTICATION

A token is a piece of data that has no meaning or use on its own, but combined with the correct tokenization system, becomes a vital player in securing your application. Token based authentication works by ensuring that each request to a server is accompanied by a signed token which the server verifies for authenticity and only then responds to the request.

JSON Web Token \(JWT\) is an open standard \(RFC 7519\) that defines a compact and self-contained method for securely transmitting information between parties encoded as a JSON object. JWT has gained mass popularity due to its compact size which allows tokens to be easily transmitted via query strings, header attributes and within the body of a POST request.

### WHY USE TOKENS?

The use of tokens has many benefits compared to traditional methods such as cookies.

{% hint style="success" %}
**Tokens are stateless.** The token is self-contained and contains all the information it needs for authentication. This is great for scalability as it frees your server from having to store session state.
{% endhint %}

{% hint style="success" %}
**Tokens can be generated from anywhere.** Token generation is decoupled from token verification allowing you the option to handle the signing of tokens on a separate server or even through a different company such us Auth0.
{% endhint %}

{% hint style="success" %}
**Fine-grained access control.** Within the token payload you can easily specify user roles and permissions as well as resources that the user can access.
{% endhint %}

These are just some of the benefits JSON Web Tokens provide.

### ANATOMY OF A JSON WEB TOKEN

A JSON Web Token consists of three parts: **Header**, **Payload** and **Signature**. The header and payload are Base64 encoded, then concatenated by a period, finally the result is algorithmically signed producing a token in the form of header.claims.signature. The header consists of metadata including the type of token and the hashing algorithm used to sign the token. The payload contains the claims data that the token is encoding. The final result looks like:

```text
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJtZXNzYWdlIjoiSldUIFJ1bGVzISIsImlhdCI6MTQ1OTQ0ODExOSwiZXhwIjoxNDU5NDU0NTE5fQ.-yIVBD5b73C75osbmwwshQNRC7frWUYrqaTjTpza2y4
```

Tokens are signed to protect against manipulation, they are not encrypted. What this means is that a token can be easily decoded and its contents revealed. If we navigate over the jwt.io, and paste the above token, we’ll be able to read the header and payload – but without the correct secret, the token is useless and we see the message “Invalid Signature.” If we add the correct secret, in this example, the string L3@RNJWT, we’ll now see a message saying “Signature Verified.”

![](../../.gitbook/assets/screen-shot-2016-04-04-at-10.07.29-am-1024x728.png)

In a real world scenario, a client would make a request to the server and pass the token with the request. The server would attempt to verify the token and, if successful, would continue processing the request. If the server could not verify the token, the server would send a 401 Unauthorized and a message saying that the request could not be processed as authorization could not be verified.

### JSON WEB TOKEN BEST PRACTICES

Before we actually get to implementing JWT, let’s cover some best practices to ensure token based authentication is properly implemented in your application.

* **Keep it secret. Keep it safe.** The signing key should be treated like any other credentials and revealed only to services that absolutely need it.
* **Do not add sensitive data to the payload.** Tokens are signed to protect against manipulation and are easily decoded. Add the bare minimum number of claims to the payload for best performance and security.
* **Give tokens an expiration.** Technically, once a token is signed – it is valid forever – unless the signing key is changed or expiration explicitly set. This could pose potential issues so have a strategy for expiring and/or revoking tokens.
* **Embrace HTTPS.** Do not send tokens over non-HTTPS connections as those requests can be intercepted and tokens compromised.
* **Consider all of your authorization use cases.** Adding a secondary token verification system that ensure tokens were generated from your server, for example, may not be common practice, but may be necessary to meet your requirements.

### USE CASES FOR TOKEN BASED AUTHENTICATION

To conclude, let’s examine use cases where token based authentication is best suited for.

* **Platform-as-a-Service Applications** – exposing RESTful APIs that will be consumed by a variety of frameworks and clients.
* **Mobile Apps** – implementing native or hybrid mobile apps that interact with your services.
* **Single Page Applications \(SPA\)** – building modern applications with frameworks such as Angular and React.

