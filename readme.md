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
