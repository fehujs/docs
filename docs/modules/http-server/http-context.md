# Http context

The http context is an object containing the response and the request during the request travel into our server. It's created when the server get receive the request, and the response is what you'll return to the client.

It contains a optional `req` instance that is the request from Node HTTP module, which is an ``IncomingMessage``, for more informations, please refer to the [official Nodejs documentation](https://nodejs.org/api/http.html#class-httpincomingmessage).

## Request

You can create a new instance (if you want) by calling the `Request.init()` static method, but the server creates it automatically.

This class has a lot of getters that permits you to access to the request data. See the implementation for more infos.

## Response

The response is what you'll send to the client, so you need to know how it works.

The server creates it automatically like Request, and your "job" is to find what you have to put in it.

There's a lot of getters and setters on this class, see the implementation for more infos.
