<div style="width: 100%;display:flex;justify-content: center">
    <img alt="Fehujs" src="https://raw.githubusercontent.com/fehujs/logos/refs/heads/main/fehu-banner.png" />
</div>

# Fehujs documentation

Welcome on the official documentation website of fehujs.

## About the project

This is a project built by a french student for educational purposes. It isn't meant to be used in real production contexts, but to understand how a big open source project could be organized & how APIs and web servers works.

Fehu is a rune, you can learn more about it on [Wikipedia](https://en.wikipedia.org/wiki/Fehu).

## Organization

The project is organized of many different modules that are designed to be the most independent, with as few external dependencies as possible.

### Modules

- [create-fehu-app](https://github.com/fehujs/create-fehu-app): create fehu app module
- [@fehujs/auth](https://github.com/fehujs/auth): User authentication build-in module for Fehujs apps
- [@fehujs/csrf-shield](https://github.com/fehujs/csrf-shield): CSRF protection module
- [@fehujs/database](https://github.com/fehujs/database): Fehujs database package
- [@fehujs/fcli](https://github.com/fehujs/fcli): Fehujs script runner
- [@fehujs/helpers](https://github.com/fehujs/helpers): Fehujs utilitaries (contains file handling, parsing helpers, and id generation)
- [@fehujs/http-server](https://github.com/fehujs/http-server): HTTP server for fehujs projects
- [@fehujs/ioc](https://github.com/fehujs/ioc): IoC container / dependency injection module for fehujs project
- [@fehujs/jeran](https://github.com/fehujs/jeran): Fehujs apps command launcher
- [@fehujs/sessions](https://github.com/fehujs/sessions): Fehujs sessions handling package (only handles session ids yet)
- [@fehujs/template-parser](https://github.com/fehujs/template-parser): Small template parser
- [@fehujs/validator](https://github.com/fehujs/validator): Object validator for requests

### Internal modules

These modules are internal helpers for Fehujs apps development:

- [@fehujs/build](https://github.com/fehujs/build): Fehujs build utility, it serves to bundle & build the different packages.
- [@fehujs/tsconfig](https://github.com/fehujs/tsconfig): TS config base for FehuJS projects

