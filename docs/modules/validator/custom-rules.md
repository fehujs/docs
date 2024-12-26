# Validators directory

You can set your schemas in files contained into `src/app/validators`.

## Create custom rules

If you want to create a custom rule, you can create a file named `rules.ts` into `src/app/validators`.

Then, begin to implement your rules!

```ts
import type { Rule } from "@fehujs/validator"

export const customRule = (str: string) => {
    return {
        name: "Custom rule name",
        errMsg: "Custom rule error message",
        cb: () => {
            if (/** your condition */) return true

            return false
        }
    } as Rule
}
```

Now you can easily use this rule in your schemas:

```ts
    // ...
    "customRule": [],
    // ...
```

!!! info
    The first argument of the function is provided by the module, so in the schema declaration you __MUST NOT__ set it as a rule param. But the next arguments MUST be set into the schema declaration.

Here's an example:

```ts
export const myCustomMin = (str: string, min: number, foo: string) => {
    return {
        name: "Custom minimum string length",
        errMsg: "The string isn't long enough (custom rule)",
        cb: () => {
            console.log(foo)

            if (str.length >= min) return true

            return false
        }
    } as Rule
}
```

As you can see, we added a parameter named `min` and another named `foo`. In the schema, the declaration would look like this:
```ts
    // ...
    "myCustomMin": [
        8, // min param
        "bar" // foo param
    ],
    // ...
```

!!! note
    Please note that the params are handled in the order of declaration, do not put the foo param before the min param.
