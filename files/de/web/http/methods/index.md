---
title: HTTP request methods
slug: Web/HTTP/Methods
tags:
  - HTTP
  - Methods
  - NeedsTranslation
  - Reference
  - TopicStub
translation_of: Web/HTTP/Methods
---
{{HTTPSidebar}}

HTTP defines a set of **request methods** to indicate the desired action to be performed for a given resource. Although they can also be nouns, these request methods are sometimes referred as _HTTP verbs_. Each of them implements a different semantic, but some common features are shared by a group of them: e.g. a request method can be {{glossary("safe")}}, {{glossary("idempotent")}}, or {{glossary("cacheable")}}.

- [`GET`](/en-US/docs/Web/HTTP/Methods/GET)
  - : The `GET` method requests a representation of the specified resource. Requests using `GET` should only retrieve data.
- [`HEAD`](/en-US/docs/Web/HTTP/Methods/HEAD)
  - : The `HEAD` method asks for a response identical to that of a `GET` request, but without the response body.
- [`POST`](/en-US/docs/Web/HTTP/Methods/POST)
  - : The `POST` method is used to submit an entity to the specified resource, often causing a change in state or side effects on the server.
- [`PUT`](/en-US/docs/Web/HTTP/Methods/PUT)
  - : The `PUT` method replaces all current representations of the target resource with the request payload.
- [`DELETE`](/en-US/docs/Web/HTTP/Methods/DELETE)
  - : The `DELETE` method deletes the specified resource.
- [`CONNECT`](/en-US/docs/Web/HTTP/Methods/CONNECT)
  - : The `CONNECT` method establishes a tunnel to the server identified by the target resource.
- [`OPTIONS`](/en-US/docs/Web/HTTP/Methods/OPTIONS)
  - : The `OPTIONS` method is used to describe the communication options for the target resource.
- [`TRACE`](/en-US/docs/Web/HTTP/Methods/TRACE)
  - : The `TRACE` method performs a message loop-back test along the path to the target resource.
- [`PATCH`](/en-US/docs/Web/HTTP/Methods/PATCH)
  - : The `PATCH` method is used to apply partial modifications to a resource.

## Specifications

| Specification                                        | Title                                                         | Comment                                                          |
| ---------------------------------------------------- | ------------------------------------------------------------- | ---------------------------------------------------------------- |
| {{RFC("7231", "Request methods", "4")}} | Hypertext Transfer Protocol (HTTP/1.1): Semantics and Content | Specifies GET, HEAD, POST, PUT, DELETE, CONNECT, OPTIONS, TRACE. |
| {{RFC("5789", "Patch method", "2")}}     | PATCH Method for HTTP                                         | Specifies PATCH.                                                 |

## Browser compatibility

{{Compat("http/methods")}}

## See also

- [HTTP headers](/de/docs/Web/HTTP/Headers)
