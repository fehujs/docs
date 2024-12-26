# Usage

Here's a sign up view process using the validator module:

```ts
    const schema = await Schema.create({
        name: {
            "optional": ["John Doe"]  // (1)!
        },
        email: {
            "email": []
        },
        password: {
            "min": [8]
        }
    })
    const body = await schema.parse<SignupPayload>(await getPostBody(req))
    let user: ModelObject | null

    if (!body.success) {
        // error: the body doesn't math with the schema 
    }

    try {
        user = await User.create({
            name: body.data.name,
            email: body.data.email,
            password: body.data.password
        })
    } catch (err: any) {
        // error: error while creating user (email already taken, ...)
    }
```

1. You can set a default value if you want (if the field is empty, the default value will be set).

The first part consists to defining our schema. The schema is an object which keys will be the fields of the parsed object (here, the request body). In each key, you can put an object containing the rules that the field must comply with.

A simple draft of what it means:
```ts
{
    field1: {
        rule1: ["rule1 param1", "rule1 param2"]
        rule2: ["rule2 param1"]
    },
    field2: {
        rule3: []
    }
}
```

Then comes the request parsing: `await schema.parse<SignupPayload>(request.body)`

You specify in parameters of the async method `schema.parse()` the object to parse, and you must provide the output type.

Let's say that 
```ts
type SignupPayload = {
    name: string
    email: string
    password: string
}
```

To the `schema.parse()` output will be typed as

```ts
{
    success: boolean
    data: SignupPayload
}
```

So you can verify if the parsing is a success or not with `success`.

If the parsing is a success, you can get the parsed data by accessing to (in this example) `body.data`.

!!! note
    If the parsing isn't valid, the `data` object will contain the errors of each field.

    E.g: if the request body was something like 
    ```
    {
        email: "e",
        password: "123"
    }
    ```

    the `schema.parse()` return would be

    ```
    {
        success: false,
        data: {
            name: "",
            email: "Invalid email",
            password: "Text isn't long enough, excepted a 8 characters minimum text"
        }
    }
    ```
