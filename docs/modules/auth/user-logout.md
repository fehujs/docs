# User logout

Some code from a logout view:
```ts
    const user = await User.getCurrentUser(request)
    response = await User.logout({ request, response }, user!) // (1)!
    return response.redirect("/users/login")
```

1. Here we suppose that this view has the `AuthMiddleware`.

First of all, we get the current user logged in with the `User.getCurrentUser()` method (we'll use this method to get the current user if we need them).

Then, we call `User.logout()`, that will suppress the auth token cookie and the token in the database too.
