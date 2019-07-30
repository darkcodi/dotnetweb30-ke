# Implement caching

### Response caching

Response caching reduces the number of requests a client or proxy makes to a web server. Response caching also reduces the amount of work the web server performs to generate a response. Response caching is controlled by headers that specify how you want client, proxy, and middleware to cache responses.

The ResponseCache attribute participates in setting response caching headers, which clients may honor when caching responses. Response Caching Middleware can be used to cache responses on the server. The middleware can use ResponseCacheAttribute properties to influence server-side caching behavior.

### HTTP-based response caching

The HTTP 1.1 Caching specification describes how Internet caches should behave. The primary HTTP header used for caching is Cache-Control, which is used to specify cache directives. The directives control caching behavior as requests make their way from clients to servers and as responses make their way from servers back to clients. Requests and responses move through proxy servers, and proxy servers must also conform to the HTTP 1.1 Caching specification.

Common Cache-Control directives are shown in the following table:

| [public](https://tools.ietf.org/html/rfc7234#section-5.2.2.5) | A cache may store the response. |
| :--- | :--- |
| [private](https://tools.ietf.org/html/rfc7234#section-5.2.2.6) | The response must not be stored by a shared cache. A private cache may store and reuse the response. |
| [max-age](https://tools.ietf.org/html/rfc7234#section-5.2.1.1) | The client doesn't accept a response whose age is greater than the specified number of seconds. Examples: `max-age=60` \(60 seconds\), `max-age=2592000` \(1 month\) |
| [no-cache](https://tools.ietf.org/html/rfc7234#section-5.2.1.4) | **On requests**: A cache must not use a stored response to satisfy the request. The origin server regenerates the response for the client, and the middleware updates the stored response in its cache. **On responses**: The response must not be used for a subsequent request without validation on the origin server. |
| [no-store](https://tools.ietf.org/html/rfc7234#section-5.2.1.5) | **On requests**: A cache must not store the request. **On responses**: A cache must not store any part of the response. |

### Other caching technology in ASP.NET Core

#### In-memory caching

In-memory caching uses server memory to store cached data. This type of caching is suitable for a single server or multiple servers using sticky sessions. Sticky sessions means that the requests from a client are always routed to the same server for processing.

For more information, see [Cache in-memory in ASP.NET Core](https://docs.microsoft.com/en-us/aspnet/core/performance/caching/memory?view=aspnetcore-2.2).

#### Distributed Cache

Use a distributed cache to store data in memory when the app is hosted in a cloud or server farm. The cache is shared across the servers that process requests. A client can submit a request that's handled by any server in the group if cached data for the client is available. ASP.NET Core offers SQL Server and Redis distributed caches.

For more information, see [Distributed caching in ASP.NET Core](https://docs.microsoft.com/en-us/aspnet/core/performance/caching/distributed?view=aspnetcore-2.2).

#### Cache Tag Helper

Cache the content from an MVC view or Razor Page with the Cache Tag Helper. The Cache Tag Helper uses in-memory caching to store data.

For more information, see [Cache Tag Helper in ASP.NET Core MVC](https://docs.microsoft.com/en-us/aspnet/core/mvc/views/tag-helpers/built-in/cache-tag-helper?view=aspnetcore-2.2).

#### Distributed Cache Tag Helper

Cache the content from an MVC view or Razor Page in distributed cloud or web farm scenarios with the Distributed Cache Tag Helper. The Distributed Cache Tag Helper uses SQL Server or Redis to store data.

For more information, see [Distributed Cache Tag Helper in ASP.NET Core](https://docs.microsoft.com/en-us/aspnet/core/mvc/views/tag-helpers/built-in/distributed-cache-tag-helper?view=aspnetcore-2.2).

{% hint style="warning" %}
Disable caching for content that contains information for authenticated clients. Caching should only be enabled for content that doesn't change based on a user's identity or whether a user is signed in.
{% endhint %}

