# Assets

## `public` directory

All files contained in the public directory will be registered as GET endpoints by the server thanks to the Assets Helper on the server startup.

The endpoint url will be the relative path of the file from `./src/public`.

If the file extension isn't in the `./src/content-types.json` file, please add it yourself (it will be served as plain text otherwise).
