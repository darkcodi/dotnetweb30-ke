# API versioning

Change is inevitable and growth is a good thing. When your API has reached the point of expanding beyond it’s original intent and capacity, it’s time to consider the next version.

Whether that next iteration is a whole number version bump or just a feature expansion, it’s important to consider the pros and cons of how you let your developers know about it. Far different than traditional software versioning, API versioning can have complex implications for the products using it downstream.

### When to Version

APIs only need to be up-versioned when a breaking change is made. Breaking changes include:

* a change in the format of the response data for one or more calls
* a change in the response type \(i.e. changing an integer to a float\)
* removing any part of the API.

**Breaking changes** should always result in a change to the major version number for an API or content response type.

**Non-breaking changes**, such as adding new endpoints or new response parameters, do not require a change to the major version number. However, it can be helpful to track the minor versions of APIs when changes are made to support customers who may be receiving cached versions of data or may be experiencing other API issues.

### How to Version

REST doesn’t provide for any specific versioning guidelines but the more commonly used approaches fall into four categories.

#### Versioning through URI Path

Using the URI is the most straightforward approach \(and most commonly used as well\) though it does violate the principle that a URI should refer to a unique resource. You are also guaranteed to break client integration when a version is updated.

```text
http://api.example.com/v1
http://apiv1.example.com
```

The version need not be numeric, nor specified using the “v\[x\]” syntax. Alternatives include dates, project names, seasons or other identifiers that are meaningful enough to the team producing the APIs and flexible enough to change as the versions change.

#### Versioning through query parameters

Another option for versioning a REST API is to include the version number as a query parameter. This is a straightforward way of versioning an API from an implementation point of view. It is also easy to default to the latest version if a query parameter is not specified.

The main drawback comparing to the URI versioning is the difficulty of routing. Query parameters are in fact more difficult to use for routing requests to the proper API version.

```text
http://www.example.com/api/products?version=1
```

#### Versioning using Custom Request Header

A custom header \(e.g. Accept-version\) allows you to preserve your URIs between versions though it is effectively a duplicate of the content negotiation behavior implemented by the existing Accept header.

```text
Accept-version: v1
Accept-version: v2
```

#### Versioning using Accept header

Content negotiation may let you preserve a clean set of URLs but you still have to deal with the complexity of serving different versions of content somewhere. This burden tends to be moved up the stack to your API controllers which become responsible for figuring out which version of a resource to send. The end result tends to be a more complex API as clients have to know which headers to specify before requesting a resource.

```text
Accept: application/vnd.example.v1+json
Accept: application/vnd.example+json;version=1.0
```

In the real world, an API is never going to be completely stable. So it’s important how this change is managed. A well documented and gradual deprecation of API can be an acceptable practice for most of the APIs.

