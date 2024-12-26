# User login

There's an example of a login view:
```ts
    const body = request.body
    let user: User | null
    
    // body validation

    try {
        user = await User.verifyCrendentials(body.email, body.password)
    } catch (err: any) {
        // some errors could happen here
    }

    if (user) {
        response = await User.login({ request, response }, user)
        return response.redirect("/users/dashboard")
    }

    // wrong credentials handling
```

As you can see, we're using `User.login()` here as well.

Now, let's have a look about `User.verifyCredentials()`. This method will verify if the password provided by the user matches with the password of the user identified by it's email. The method will return the user if they match, `null` else.
