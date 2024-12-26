# Middlewares

Middlewares are methods that are executed before the route code and permits to do some checks about the request.

If you want to know if a user is logged in or not, you'll need to implement a middleware (I mean, you can do this in a controller but it's not as clean as with middlewares because you might use the same code in other routes etc...).

You can create a file at `src/app/middlewares` and type this code in the the file:

for example:
```ts
import { Middleware, HttpContext } from "@fehujs/http-server"


export class MyMiddleware extends Middleware {
    public async handle(httpContext: HttpContext) {
        console.log("my middleware")
        return super.handle(httpContext)
    }
}
```

The `super.handle()` intruction will call the next middleware or return the output Http context at the end of middleware execution process (you can edit the ``request`` in the middlewares).

Now you can register it in routes (cf. [Route page](routing.md)).

If the '/' route is called, the middleware will be runned before the route code and the middleware can decide if the process continues or no.

There's an example of a middleware that decides to return the response right after it's execution:

```ts
export class TestMiddleware extends Middleware {
    public async handle(httpContext: HttpContext) {
        console.log("authorization middleware")
        const isAuthorized = false  // this is only an example

        if (isAuthorized) {
            return super.handle(httpContext)
        }

        httpContext.response.setErrorResponse({
            statusCode: 403,
            statusMessage: "Unauthorized"
        })
        return httpContext
    }
}
```

!!! note
    In the case where ``isAuthorized`` is false, we define a response that will be returned directly after the calling of this middleware because we return the Http context and not the next middleware.

!!! warning
    Please note that in the "middleware" response context (aka when the middlewares are processed), if you call the response's methods ``redirect``, ``setResponse`` or ``setErrorRespone``, the view after the middleware won't be runned and the response from the last runned middleware will be send to the client.

You can also do the last example using ``MiddlewareError``:

```ts
export class TestMiddleware extends Middleware {
    public async handle(httpContext: HttpContext) {
        console.log("authorization middleware")
        const isAuthorized = false

        if (isAuthorized) {
            return super.handle(httpContext)
        }

        throw new MiddlewareError(403, "Not authorized", "Unauthorized")
    }
}
```

The ``MiddlewareError`` will be catched and it will return the response specified in the exception:
- responseStatus: should be an error HTTP status code
- responseMsg: the body of the error response
- message: the error description
- contentType: default = "text/html"
