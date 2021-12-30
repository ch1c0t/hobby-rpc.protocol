# Introduction

Hobby-RPC is a request-response protocol over [HTTP messages][HTTP].

Clients send JSON in [the POST request][POST]'s body and receive JSON in the response.
They can call nullary and unary functions.

[HTTP]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Messages
[POST]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/POST

## Nullary functions

To call a nullary function, a client should pass a function name(as the `fn` property).
For example, to call a function named `SomeNullaryFunction` with `curl`:

```
curl -H "Content-Type: application/json" -X POST -d '{"fn":"SomeNullaryFunction"}' https://some.domain
```

## Unary functions

To call an unary function, a client should pass a function name(as the `fn` property) and its input(as the `in` property).
For example, to call a function named `SomeUnaryFunction` with `curl`:

```
curl -H "Content-Type: application/json" -X POST -d '{"fn":"SomeUnaryFunction","in":42}' https://some.domain
```

## Responses

Servers can respond with:

- [200 OK][200]:

  Happy path and JSON output in the body.

- [400 Bad Request][400]:

  Something is wrong with the request.
  It could be a malformed JSON, or the Content-Type which doesn't start with 'application/json', or something else.

- [403 Forbidden][403]:

  [The Authorization header][Authorization] doesn't contain a valid token.

[200]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/200
[400]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/400
[403]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/403
[Authorization]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Authorization

## Authorization

Servers may choose to require clients to be authorized.
In such cases, they will forbid any requests except those with valid tokens.

Clients may pass tokens as follows:

```
curl -H "Content-Type: application/json" -H "Authorization: SomeToken" -X POST -d '{"fn":"SomeNullaryFunction"}' https://some.domain
```

# Implementations

## Servers

- [Node.js](https://github.com/ch1c0t/hobby-rpc.servers.nodejs)
- [Ruby](https://github.com/ch1c0t/hobby-rpc)

## Clients

- [A client for web browsers](https://github.com/ch1c0t/hobby-rpc.clients.js)
