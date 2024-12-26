# Usage

There's some examples of how we could use this module

```js title="./scripts/build.cjs"
const build = require("@fehujs/build")

build()
```

## Reference

### ``build(mainPath = "./src/index.ts", tsconfigPath = "./tsconfig.json")``

This is the function that bundles and build a TypeScript project.

It uses [esbuild](https://esbuild.github.io/) under the hood.
