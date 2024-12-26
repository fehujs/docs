# Migrations

The migrations can help you to define the tables of your database.

## Create a migration

You have to create a new file in the `src/db/migrations` directory. For this example we will create a Post migration.

So, here's my migration:

```ts title="add-post.ts"
import { BaseMigration, provider, Table } from "@fehujs/database"

export class AddPostMigration extends BaseMigration {
    readonly name = "add_post"

    protected table = {
        name: "posts",
        columns: [
        ]
    }

    public async up() {
    }

    public async down() {
    }
}
```

### Define tables

To define tables, you have to put columns into your table. Watch out:

```ts title="add-post.ts"
// ...

export class AddPostMigration extends BaseMigration {
    readonly name = "add_post"

    protected table = {
        name: "posts",
        columns: [
            {
                name: 'id',
                type: 'INTEGER',
                isNotNull: true,
                isPrimaryKey: true,
                isUnique: true,
                // isAutoincrement: true  (1)
            },
            {
                name: 'title',
                type: 'TEXT',
                isNotNull: true
            },
            {
                name: 'content',
                type: 'TEXT',
                isNotNull: true,
            }
        ]
    }

    // ...
```

1. Nota: I won't use autoincrement to handle ids in this example

Nota: here's the column typing:
```ts
type Column = {
    name: string
    /** type of the contained value */
    type: 'TEXT' | 'INTEGER' | 'NULL' | 'REAL' | 'BLOB'
    default?: string
    isAutoIncrement?: boolean
    isNotNull?: boolean
    isPrimaryKey?: boolean
    isUnique?: boolean
}
```

Don't forget to create the `up()` and `down()` methods, the first one to set the migration up, and the second to cancel it.

```ts
import provider from "../providers" // (1)!

    // ...
    public async up() {
        await provider.createTable(this.table)
    }
    
    public async down() {
        await provider.dropTable(this.tableName)
    }
```

1. You need to export the instance of the database provider in `./src/db/providers/index.js`

!!! note "About database providers"
    ```js title="./src/db/providers/index.js"
    import { SQLiteDatabaseProvider } from "@fehujs/database"

    export const provider = new SQLiteDatabaseProvider()
    ```

    In the `providers` directory you can implement others providers for other types of databases. But don't forget to update the provider's name in the database config.

### Drop

You can drop a table using `await provider.dropTable(this.tableName)`.

### Run migrations

Now we finished implementing your migration, we want to run it.

If your migration is located in `./src/db/migrations`, it will be registered automatically.

Otherwise, you'll need to import the class and to instanciate manually:


```ts title="./bin/migrate.ts"
import { AddPostMigration } from "./add_post"

const migrations: Record<string, BaseMigration> = {
    ...(await loadAndInstanciateMigrations()),
    "add_post": new AddPostMigration(),
}
//...
```

Then you can run the migration: ``node fcli migrate``.

Nota: flags.

You can specify the migration key (from the migrations object from `./bin/migrate.ts`), and set it on up if you want to run this migration.

Example (in this case): `node fcli migrate add_post=up`, but you can put `add_post=down`. If it isn't specified, nothing happends.

If you don't put any flag, all registred migrations that were not runned (their names aren't situated in the migrations.json at the root of the project) will be runned (mode up). If you specify a key, only the migration.s specified will be executed.

### Alter table

This isn't implemented.
