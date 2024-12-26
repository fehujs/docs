# Demonstration

In `./src/app/controllers/template-demo.ts`:
```ts
export class TemplateDemoController {
    public async view({ request, response}: HttpContext): Promise<Response> {
        const messagesSent = 3
        return response.setResponse({
            contentType: "text/html",
            body: render("./src/templates/demo.html", {
                name: "john doe",
                text: "hello, world!",
                messagesSent: messagesSent,
                msgs: ["hi", "hi1", "hi2"],
                isSentALotOfMsg: messagesSent > 3  // (1)!
            })
        })
    }
}
```

1. Nota: conditions aren't supported inside of the template, so put the condition into a variable and do a condition as '{{#if condition}} ...'

In `./src/templates/demo.html`:
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Template Demo</title>

    <!-- ... -->
</head>
<body>
    <h3>Hi, {{name}}!</h3>
    <p>{{text}}</p>

    {{#if msgs}}
        {{#for msg in msgs}}
            <p>{{msg}}</p>
        {{/for}}
    {{/if}}

    <!-- (1)! -->
    {{#include src/templates/component.html}}
        <p>Couldn't load component.html</p>
    {{/include}}

    <script src="/app.js"></script>
</body>
</html>
```

1. Nota: if the parser couldn't load the component, it will display the block of code between its tags

And `./src/templates/conponent.html`:
```html
<pre>./src/templates/component.html</pre>

<!-- as you can see, the included templates inherits of the main context -->
<!-- as I said above, make a condition like this with the condition variable -->
{{#if isSentALotOfMsg}}
    <p>You sent us a lot of messages ({{messagesSent}}), thanks</p>
{{/if}}
```

With this example, we get this response:
```html
    <!-- ... -->

    <h3>Hi, john doe!</h3>
    <p>hello, world!</p>

    

    
        
            <p>hi</p>
        
            <p>hi1</p>
        
            <p>hi2</p>
        
    

    <pre>./src/templates/component.html</pre>
    

<p>You sent us a lot of messages (4), thanks</p>
<pre>from component</pre>

    <!-- ... -->
```
