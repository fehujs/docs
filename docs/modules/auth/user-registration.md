# User registration

Here's a demonstration of a view that creates a user:
```ts
    const body = request.body
    let user: User | null

    // body validation

    try {
        user = await User.create({
            name: body.name,
            email: body.email,
            password: body.password
        }) as User
    } catch (err: any) {
        // error handling
    }

    response = await User.login({ request, response }, user)
    return response.redirect("/users/dashboard")
```

Please note that the creation part is quite standart, let's focus on the `User.login({ request, response }, user)`.

This method sets a cookie containing the authentication token after a user login. This cookie will serve to the auth middleware to see if the user is allowed to access to a page (it will get the token out of it and then try to get the user). Furthermore, the token will be stored in the database.
