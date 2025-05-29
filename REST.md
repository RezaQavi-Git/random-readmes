# REST API Desing Best Practice

# Design
Identifier Design with URIs: Uniform Resource Identifier (URI) is a syntax to assign a unique id to each web resource, e.g.
- Forward slash separator (/) must be used to indicate a hierarchical relationship.
- A trailing forward slash (/) should not be included in URIs.
- Hyphens (-) should be used to improve the readability of URIs.
- Underscores (_) should not be used in URIs.
- Lowercase letters should be preferred in URI paths.
- File extensions should not be included in URIs

Resource Modeling: URI conveys a REST API resource model, with each forward slash-separated path segment corresponding to a unique resource within the model’s hierarchy.

Resource Archetypes
1. `Document`: a singular concept that is akin to an object instance or database record.
2. `Collection`: server-managed directory of resources.
3. `Store`: client-managed resource repository, put resources in, get them back out, and decide when to delete them.
4. `Controller`: executable functions, with parameters and return values; inputs and outputs. Not CRUD

## HTTP Request Methods
- `GET` and `POST` must not be used to tunnel other request methods.
- `GET` must be used to retrieve a representation of a resource.
- `HEAD` should be used to retrieve response headers — Info about a resource (version/length/type).
- `OPTIONS` should be used to retrieve metadata that describes resources available interactions — Info about API (methods/content type).
- `PUT` must be used to both insert and update a stored resource.
- `POST` must be used to create a new resource in a collection.
- `POST` must be used to execute controllers.
- `DELETE` must be used to remove a resource from its parent.

## Response Status Codes
- `200` (“OK”) should be used to indicate nonspecific success.
- `200` (“OK”) must not be used to communicate errors in the response body.
- `201` (“Created”) must be used to indicate successful resource creation.
- `202` (“Accepted”) must be used to indicate the successful start of an asynchronous action
- `204` (“No Content”) should be used when the response body is intentionally empty.
- `301` (“Moved Permanently”) should be used to relocate resources.
- `302` (“Found”) should not be used.
- `303` (“See Other”) should be used to refer the client to a different URI.
- `304` (“Not Modified”) should be used to preserve bandwidth.
- `307` (“Temporary Redirect”) should be used to tell clients to resubmit the request to another URI.
- `400` (“Bad Request”) may be used to indicate nonspecific failure.
- `401` (“Unauthorized”) must be used when there is a problem with the client’s credentials.
- `403` (“Forbidden”) should be used to forbid access regardless of the authorization state.
- `404` (“Not Found”) must be used when a client’s URI cannot be mapped to a resource.
- `405` (“Method Not Allowed”) must be used when the HTTP method is not supported.
- `406` (“Not Acceptable”) must be used when the requested media type cannot be served.
- `409` (“Conflict”) should be used to indicate a violation of the resource state.
- `412` (“Precondition Failed”) should be used to support conditional operations.
- `415` (“Unsupported Media Type”) must be used when the media type of a request payload cannot be processed.

## Metadata Design
- `Content-Type` must be used.
- `Content-Length` should be used. First, a client can know whether it has read the correct number of bytes from the connection. Second, a client can make a HEAD request to find out how large the entity-body is, without downloading it
- `Last-Modified` should be used in responses. A timestamp that indicates the last time that something happened to alter the representational state of the resource.
- `Cache-Control`, Expires, and Date response headers should be used to encourage caching.
- `Cache-Control`, Expires, and Pragma response headers may be used to discourage caching. 


## Rules
- URI Path Design
    - A singular noun should be used for document names.
    - A plural noun should be used for collection names.
    - A verb or verb phrase should be used for controller names.
    - Variable path segments may be substituted with identity-based values.
    - CRUD function names should not be used in URIs.
- URI Query Design
    - The query component of a URI may be used to filter collections or stores.
    - The query component of a URI should be used to paginate collection or store results.
- Accept and respond with JSON
- Use nouns instead of verbs in endpoint paths
    - We shouldn't use verbs in our endpoint paths. Instead, we should use the nouns which represent the entity that the endpoint that we're retrieving or manipulating as the pathname.
- Use logical nesting on endpoints
    - When designing endpoints, it makes sense to group those that contain associated information. That is, if one object can contain another object, you should design the endpoint to reflect that. This is good practice regardless of whether your data is structured like this in your database
- Handle errors gracefully and return standard error codes
    - To eliminate confusion for API users when an error occurs, we should handle errors gracefully and return HTTP response codes that indicate what kind of error occurred.
- Allow filtering, sorting, and pagination


## References
- [medium.com](https://medium.com/@ibrahimsoliman97/summary-of-rest-api-design-rulebook-by-mark-mass%C3%A9-6f290fa04a2d)
- [REST API Design Rulebook](https://www.oreilly.com/library/view/rest-api-design/9781449317904/)
- [stackoverflow.blog](https://stackoverflow.blog/2020/03/02/best-practices-for-rest-api-design/)