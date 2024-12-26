# Cookies

The ``Request`` class has a ``cookieHandler`` property which returns a ``CookieHandler``.

You won't need to create an instance yourself (as for ``Request`` or ``Response``).

## ``getCookies(): Record<string, string>``

Get all the cookies from the response.

## ``getCookie(name: string): string``

Get the value of the specified cookie.

## ``setCookie(response: Response, cookie: Cookie): Response``

Creates a cookie. 

!!! warning
    This method adds a header in the response, so you need to assign the new headers on your response.
    
    E.g: `response = request.cookieHandler.setCookie(response, cookie)`

```ts title="This is the type of a cookie"
export type Cookie = {
    name: string
    value: string
    domain?: string
    expires?: string
    httpOnly?: boolean
    maxAge?: number
    partitioned?: boolean
    path?: string
    secure?: boolean
    sameSite?: "Strict" | "Lax" | "None"
}
```

## ``deleteCookie(response: Response, name: string): Response``

Deletes a cookie.

!!! warning
    This method adds a header in the response, so you need to assign the new headers on your response.

    E.g: `response = request.cookieHandler.deleteCookie(response, cookieName)`
