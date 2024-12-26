# Reference

## `render(path: string, context: Context): string`

- `path`: the path of the template to parse.
- `context`: the context, in other words the variables that will serve to edit the template.

## `Context`

It is an object of string keys (the variables names) and their values. The values can be string, number, boolean and arrays of string, numbers or booleans.

## `TemplateNotFound(path: string)`

Shows an error message (in console) if a template isn't found. If it's the main template, it returns this HTML in the response: ```"<pre>[template-parser] default html template</pre>"```, if it's an included template it will inject the include tag content (please see [Block Reference > Include](block-reference.md#include) section).

## `VariableMissingInContext(varName: string)`

Shows an error (in console) if a variable called in the template isn't defined in the context.

## `WrongTypeVariable(varName: string, actualType: string, exceptedType: string)`

Shows an error (in console) if a variable isn't of the excepted type.
