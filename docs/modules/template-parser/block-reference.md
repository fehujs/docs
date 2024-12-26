# Block Reference

## Variables

Syntax:
```
{{myVar}}
```

## Conditions

Syntax:
```
{{#if myVar}}

    <!-- some code -->

{{/if}}
```

!!! bug
    Tags else if and else aren't planned to be implemented yet.

### Loops

Syntax:
```
{{#for i in myArray}}

    <!-- some code-->

{{/for}}
```

### Include

Syntax:
```
{{#include ./path/to/included/file.html}}
    <p>Couldn't load file.html</p>
{{/include}}
```

!!! tip
    If the engine can't load the file it will display the block content.

!!! tip
    The container file's context will apply to all included files.
