# @fehujs/database

This module permits you to interact with a database, to handle your migrations and your models.

For now on, only the SQLite database provider is implemented, but you can implement other providers on your own using the API (more info at the bottom of this file).

It uses [Knex](https://knexjs.org/) under the hood, but maybe we'll create a homemade SQL query builder (one day).

Please note that foreign keys aren't planned to be implemented. If you want to link two tables create a field in the first one that contains the second table primary key.

DISCLAIMER: some features are not fully available or tested (alter table, findByWithSQL, SQL injection avoider), please consider test them yourselves before using these features.

Note: you can install the SQLite Viewer VS code extension (from Florian Klampfer) to view your database directly from the IDE.

## Module configuration

- ``NAME: "database.sqlite"``
- ``PATH: "database.sqlite"``
- ``PROVIDER: "sqlite"``
- ``CONFIG`` (config is an object with the following properties):
    - ``user: 'localhost'``
    - ``host: 'localhost'``
    - ``database: "database.db"``
    - ``password: ""``
    - ``port: 5432``

## Contribute

GitHub repository: [fehujs/database](https://github.com/fehujs/database)

NPM: [@fehujs/database](https://www.npmjs.com/package/@fehujs/database)

Licence: [MIT](https://github.com/fehujs/database/blob/main/LICENSE)


## Contributors

<a href="https://github.com/fehujs/database/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=fehujs/database" />
</a>

Made with [contrib.rocks](https://contrib.rocks).
