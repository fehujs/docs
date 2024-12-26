# Contribute

This page describes more precisely how the parser works, and how you can contribute.

## Implement a new block

This parser parses templates with the help of regex.

All you have to do is adding your regex in a constant at the top of the `@fehujs/template-parser/handlers.ts`, write your handler function that calls the "replacing function" and return the template parsed.

Then you "register" your handler function into the `parse(template: string, context: string)`.

Let's see a little demonstration : how the for loops are implemented.

```ts
//...

const REGEX_FORLOOP = /{{#for\s+(\w+)\s+in\s+(\w+)}}([\s\S]*?){{\/for}}/g  // (1)!

// ...

function forLoopHandler (template: string, context: Context) {  // (2)!
    return template.replace(
        REGEX_FORLOOP,
        (match, itemName, arrayName, content) => {  // (3)!
            const items = context[arrayName]

            if (!items) new VariableMissingInContext(arrayName)

            if (Array.isArray(items)) {
                return items.map(item => {
                    const newContext = { ...context }
                    newContext[itemName] = item
                    return parse(content, newContext)
                }).join('')
            }
            new WrongTypeVariable(arrayName, typeof arrayName, "Array")
            return ''
        }
    )
}

// ...


export function parse (template: string, context: Context) {
    // ...
    template = forLoopHandler(template, context)  // (4)!
    // ...
    return template
}
```

1. The regex that parses all for loops (you can test it on https://regex101.com/)
2. The handler function
3. The "replacing function"
4. That's what I'm talking about when I say "register"

## Implement a new error

You can implement an error by writing a code like this in the `template-parser/errors.ts`:
```ts
export class MyError {
    constructor (arg1: string, arg2: string) {
        logError("MyError", `${arg1} and ${arg2} must........`)
    }
}
```
