# Router

There are the reference of the router helpers functions.

## ``patternToRegex(pattern: string): RegExp``

This fucntion permits to convert a route pattern into a regex, which will be used for the route identification at request receiving.

## ``extractRouteParams(match: RegExpMatchArray, pattern: string): RouteParams``

This function extracts the params of a route with params depending on its regex.
