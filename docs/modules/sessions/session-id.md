# Session id

The session id is is a token that permits to identify requests.

It is stored in a cookie.

You can customize the token size, and the session id cookie name and expiration date.

## ``getSessionId(request: Request)``

Get the request's session id. If it doesn't exists, create one.

## ``setSessionIdCookie({ request, response }: HttpContext)``

Set the session id cookie.
