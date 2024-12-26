# Routing

## Create a new route

You can add a new item in the `ROUTES` object of `src/app/routes.ts`:

```ts
export const ROUTES = {
    "GET:/": {
        callback: async ({ response }: HttpContext) => {
            return response.setResponse({
                contentType: "text/html",
                body: await readFile("./src/templates/index.html", "utf8")
            })
        },
    },
}
```

As you can see, the key is the endpoint of the route (if a GET request on '/' is detected, the specified callback will be called).

The callback takes a `HttpContext` parameter, and must return a `Response`. These are needed to achieve the request path into our system, from the receiving to the response sending.

If we can, we can add middlewares and route description:

```ts
export const ROUTES = {
    "GET:/": {
        callback: async ({ response }: HttpContext) => {
            return response.setResponse({
                contentType: "text/html",
                body: await readFile("./src/templates/index.html", "utf8")
            })
        },
        middlewares: [ new MyMiddleware() ],
        description: 'This is the homepage',
    },
}
```

## Routes with params

You can specify a parameter by writing `:<param name>` in the url, like in the examples below:

```ts
    "GET:/hello/:name": {
        callback: async ({ request, response }: HttpContext) => {
            return response.setResponse({
                contentType: "text/html",
                body: `Hello ${request.params.name}`
            })
        }
    },
    "GET:/hello/:name/:hi": {
        callback: async ({ request, response }: HttpContext) => {
            return response.setResponse({
                contentType: "text/html",
                body: `Hello ${request.params.name} ${request.params.hi}`
            })
        }
    },
```

If you want to access to those params in the controller, you can get them from `request.params.<param>`.

!!!bug
    You cannot have two params between two `/`.
    
    E.g: this `/post/:slug-:id` won't work. Instead do `post/:slug/:id`.

## Controllers

You can create controllers to split the code in many files.

```ts
export class CoreController extends BaseController {
    public async home({ response }: HttpContext) {
        return response.setResponse({
            contentType: "text/html",
            body: await readFile("./src/templates/index.html", "utf8")
        })
    }
}
```

And then your route is like this:

```ts
"GET:/": {
    controller: ["CoreController", "home"],
    middlewares: [ new MyMiddleware() ],
    description: 'This is the homepage',
},
```

## List routes

If you want to list all the existing routes, you can run the command ``node fcli list-routes``.
