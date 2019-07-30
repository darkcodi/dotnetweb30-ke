# Request Features

ASP.NET Core defines a number of HTTP feature interfaces in `Microsoft.AspNetCore.Http.Features` which are used by servers to identify the features they support. The following feature interfaces handle requests and return responses:

* `IHttpRequestFeature` Defines the structure of an HTTP request, including the protocol, path, query string, headers, and body.
* `IHttpResponseFeature` Defines the structure of an HTTP response, including the status code, headers, and body of the response.
* `IHttpAuthenticationFeature` Defines support for identifying users based on a `ClaimsPrincipal` and specifying an authentication handler.
* `IHttpUpgradeFeature` Defines support for HTTP Upgrades, which allow the client to specify which additional protocols it would like to use if the server wishes to switch protocols.
* `IHttpBufferingFeature` Defines methods for disabling buffering of requests and/or responses.
* `IHttpConnectionFeature` Defines properties for local and remote addresses and ports.
* `IHttpRequestLifetimeFeature` Defines support for aborting connections, or detecting if a request has been terminated prematurely, such as by a client disconnect.
* `IHttpSendFileFeature` Defines a method for sending files asynchronously.
* `IHttpWebSocketFeature` Defines an API for supporting web sockets.
* `IHttpRequestIdentifierFeature` Adds a property that can be implemented to uniquely identify requests.
* `ISessionFeature` Defines `ISessionFactory` and `ISession` abstractions for supporting user sessions.
* `ITlsConnectionFeature` Defines an API for retrieving client certificates.
* `ITlsTokenBindingFeature` Defines methods for working with TLS token binding parameters.

