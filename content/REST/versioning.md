
It is important to make sure you don't break the system for current consumers when you update your APIs.
They need to be able to use it as usual while new consumers will use the new features.
For this you need to version yout API.
There are several ways to do so.

# URI versioning

Each time you modify the web API or change the schema of resources, you add a version number to the URI for each resource. The previously existing URIs should continue to operate as before, returning resources that conform to their original schema.

Extending the previous example, if the address field is restructured into subfields containing each constituent part of the address (such as streetAddress, city, state, and zipCode), this version of the resource could be exposed through a URI containing a version number, such as https://domain-name.com/v2/customers/3:

This versioning mechanism is very simple but depends on the server routing the request to the appropriate endpoint.
it can become unwieldy as the web API matures through several iterations and the server has to support a number of different versions. Also, in all cases the client applications are fetching the same data (customer 3), so the URI should not really be different depending on the version. This scheme also complicates implementation of HATEOAS as all links will need to include the version number in their URIs.

# Query string versioning

Rather than providing multiple URIs, you can specify the version of the resource by using a parameter within the query string appended to the HTTP request, such as https://domain-name.com/customers/3?version=2. The version parameter should default to a meaningful value such as 1 if it is omitted by older client applications.

This approach has the semantic advantage that the same resource is always retrieved from the same URI, but it depends on the code that handles the request to parse the query string and send back the appropriate HTTP response. This approach also suffers from the same complications for implementing HATEOAS as the URI versioning mechanism.

# Header versioning

Rather than appending the version number as a query string parameter, you could implement a custom header that indicates the version of the resource. This approach requires that the client application adds the appropriate header to any requests, although the code handling the client request could use a default value (version 1) if the version header is omitted. The following examples use a custom header named Custom-Header. The value of this header indicates the version of web API.

GET https://domain-name.com/customers/3 HTTP/1.1
Custom-Header: api-version=1

GET https://domain-name.com/customers/3 HTTP/1.1
Custom-Header: api-version=2

As with the previous two approaches, implementing HATEOAS requires including the appropriate custom header in any links.

# Media type versioning

When a client application sends an HTTP GET request to a web server it should stipulate the format of the content that it can handle by using an Accept header, as described earlier in this guidance. Frequently the purpose of the Accept header is to allow the client application to specify whether the body of the response should be XML, JSON, or some other common format that the client can parse. However, it is possible to define custom media types that include information enabling the client application to indicate which version of a resource it is expecting.

The following example shows a request that specifies an Accept header with the value application/vnd.domain-name.v1+json. The vnd.domain-name.v1 element indicates to the web server that it should return version 1 of the resource, while the json element specifies that the format of the response body should be JSON:

GET https://domain-name.com/customers/3 HTTP/1.1
Accept: application/vnd.adventure-works.v1+json

The code handling the request is responsible for processing the Accept header and honoring it as far as possible (the client application may specify multiple formats in the Accept header, in which case the web server can choose the most appropriate format for the response body). The web server confirms the format of the data in the response body by using the Content-Type 

```
HTTP/1.1 200 OK
Content-Type: application/vnd.domain-name.v1+json; charset=utf-8

{"id":3,"name":"Contoso LLC","address":"1 Microsoft Way Redmond WA 98053"}
```

If the Accept header does not specify any known media types, the web server could generate an HTTP 406 (Not Acceptable) response message or return a message with a default media type.

This approach is arguably the purest of the versioning mechanisms and lends itself naturally to HATEOAS, which can include the MIME type of related data in resource links.

# Note

When you select a versioning strategy, you should also consider the implications on performance, especially caching on the web server. The URI versioning and Query String versioning schemes are cache-friendly inasmuch as the same URI/query string combination refers to the same data each time.

The Header versioning and Media Type versioning mechanisms typically require additional logic to examine the values in the custom header or the Accept header. In a large-scale environment, many clients using different versions of a web API can result in a significant amount of duplicated data in a server-side cache. This issue can become acute if a client application communicates with a web server through a proxy that implements caching, and that only forwards a request to the web server if it does not currently hold a copy of the requested data in its cache.

