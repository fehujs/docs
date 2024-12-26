# Server

There are the reference of the server helpers functions.

## ``getEndpoint(routes: Routes, method: string | undefined, request: Request): string``

Identifies the route depending on the request url.

## ``requestListener(options: RequestListenerOptions): Promise<void>``

This is the function that will be called when the server receive a request.

## ``runController(httpContext: HttpContext, controllers: Controllers, controller: [string, string], args?: any): Promise<Response>``

Run a controller depending on it's declaration in the route object: ``["ControllerName", "methodName"]``.

## ``runMiddlewares(httpContext: HttpContext, route: Route)``

Runs all the middlewares of the route.

## ``runView(httpContext: HttpContext, controllers: Controllers, route: Route): Promise<Response>``

Runs a view/route, if "controller" is defined, it will call ``runController``, otherwise it will call the "callback".

## ``setupControllers(): Promise<Record<string, BaseController>>``

Instanciate and resolve dependencies injections of all the controllers defined (in ``./src/app:controllers`` and ``ErrorsController``).

## ``setupRoutes(routes: Routes, globalMiddlewares: (typeof Middleware)[]): Routes``

Setup routes:

- create the regex of the endpiont pattern.
- instanciate the global middlewares and the route middlewares.
