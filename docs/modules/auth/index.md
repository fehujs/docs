# @fehujs/auth

The auth module can handle user authentication with JWT and HTTP cookies.

It uses argon2 to hash passwords and jsonwebtoken to generate the authentication tokens.

## Module configuration

There's the list of the config fields, with their default values:

- ``TOKEN_COOKIE_NAME: string = "auth_token"``
- ``TOKEN_COOKIE_EXPIRES: number = 1800000``
- ``SALT?: string = undefined``

You can override them by creating a file ``./src/config/auth.js`` which exports an object with the same attributes.

!!! warning "General warning about config overriding"
    If you decide to customize the auth module config, please override all of the items.

    Example:

    You want to add a salt:

    ```js
    export default {
      TOKEN_COOKIE_NAME = "auth_token",  // (1)!
      TOKEN_COOKIE_EXPIRES = 1800000,
      SALT = "my salt"
    }
    ```

    1. You need to rewrite the fields that you don't want to change.

    Furthermore, __you need to be at the root of the project for launching your commands__.

## Contribute

GitHub repository: [fehujs/auth](https://github.com/fehujs/auth)

NPM: [@fehujs/auth](https://www.npmjs.com/package/@fehujs/auth)

Licence: [MIT](https://github.com/fehujs/auth/blob/main/LICENSE)


## Contributors

<a href="https://github.com/fehujs/auth/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=fehujs/auth" />
</a>

Made with [contrib.rocks](https://contrib.rocks).
