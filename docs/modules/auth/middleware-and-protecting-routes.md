# Middleware & protect routes

### Auth middleware

Now let's have a look on the Auth middleware (you can learn how does a middleware in the same time):

```ts
export class AuthMiddleware extends Middleware {
    public async handle({ req, request, response}: HttpContext) {
        const user = await User.getCurrentUser(request)

        if (!user) {
            response = request.cookieHandler.deleteCookie(response, CONFIG.TOKEN_COOKIE_NAME)
            response = response.redirect("/users/login?loginRequired")
            return { req, request, response }
        }

        return super.handle({ req, request, response })
    }
}
```

So, first, it will try to get the current user. Then, if they doesn't exist, it will destroy the auth token cookie and return a redirection to the login page. If the user exists, the system will call the next middleware or the controller.

!!! note title="Middlewares"
    In the case where user is undefined, the middleware returns the Http Context instead of calling the next middleware. It's because we don't want that the request continues. If you want to reject a request from a middleware, set a middleware exception or define the response (using `response.redirect()`, `response.setResponse()` or `response.setErrorResponse()`).

    You can get more informations on the Middleware part of the documentation of the http-server module.

### Register middlewares

You can register a middleware on a route directly:

```ts
export const ROUTES: {[key: string]: Route} = {
    // ...
    "GET:/users/dashboard": {
        controller: ["UserController", "dashboard"],
        middlewares: [
            new AuthMiddleware()
        ]
    }
    // ...
}
```

You just have to add a middleware list containing all middleware.

Note: the middleware will be processed in the same order as they were set:

```ts
export const ROUTES: {[key: string]: Route} = {
    // ...
    "GET:/users/dashboard": {
        controller: ["UserController", "dashboard"],
            middlewares: [
                new AuthMiddleware(),
                new SomeMiddleware(),
            ]
        }
    }
    // ...
}
```

In this case, the `AuthMiddleware` will be called before the `SomeMiddleware`.
