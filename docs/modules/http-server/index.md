# @fehujs/http-server

This module contains the main features of a http server. It could be considered as the main module of the Fehujs project.

## Module configuration

You'll need to create a ``NODE_ENV`` variable in your ``.env`` file. This will tell to the package in which context we are running the application.

!!! note
    The only modes allowed are "dev", "test" or "production".

    If the mode isn't one of these, the "dev" will be set by default.

Furthermore, this is the others fields:
- ``port: 3000``
- ``form``:
    - ``formOptions``:
        - ``encoding: "utf-8"``
        - ``keepExtensions: true``
        - ``uploadDir: "tmp/uploads"``
    - ``errorHandler``: ``(err: any): any | undefined`` (default is ``undefined``)
- ``https: { key: string, cert: string } | undefined`` (default is ``undefined``)

!!! info "HTTPS"
    More information about HTTPS config on [this page](https.md).

!!! bug
    Please avoid importing modules into config files, because actually the config fetching doesn't support it (it doesn't support too long import promises).

You can also, in ``./src/config/global-middlewares.js``, configure a list of all the middlewares to execute before all the views.


## Contribute

GitHub repository: [fehujs/http-server](https://github.com/fehujs/http-server)

NPM: [@fehujs/http-server](https://www.npmjs.com/package/@fehujs/http-server)

Licence: [MIT](https://github.com/fehujs/http-server/blob/main/LICENSE)


## Contributors

<a href="https://github.com/fehujs/http-server/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=fehujs/http-server" />
</a>

Made with [contrib.rocks](https://contrib.rocks).
