# Usage of the providers' API

You might need to use the providers' API without models to create complex requests to your database, or for implementing new providers for other database types.

The databases providers are implementing ``DatabaseProviderInterface``:

## ``connectDb(dbPath: string): void``

Connect the DB for interaction.

## ``closeConnection(): void``

Closes the connection after transaction.

## ``get db(): any | undefined``

Returns the DB object.

## ``get dbPath(): string``

Returns the DB path.

## ``createTable: (table: CreateTable) => Promise<void>``

Permits to create a new table.

## ``alterTable: (table: AlterTable) => Promise<void>``

Permits to alter a table, usefull for migrations.

!!! warning
    `SQLiteDatabaseProvider`: not implemented yet.

### ``dropTable: (table: Table) => Promise<void>``

Drops a table.

### ``async query<T extends ModelObject>(table: Table)``

Returns a query builder.

!!! note
    ``SQLiteDatabaseProvider`` returns a new ``Knex`` instance.

### ``select <T extends ModelObject> (table: Table, condition?: any): Promise<T[]>``

Runs a select query.

!!!tip
    If you want to select all columns, don't set the them on the ``table`` argument.

    Example:

    We have a ``posts`` table with these columns: ``id``, ``title``, ``content``.

    If we want to get all these columns, you can do :
    ```ts
        const posts = await provider.select((new AddPostsMigration()).getTable(), "..") // get the cols directly specifying the table

        // OR

        const posts = await provider.select({ name: "posts" }, "...")  // create a "new table" with only the name
    ```

### ``insert <T extends ModelObject> (table: Table, value: T): Promise<T>``

Runs an insert query.

### ``update <T extends ModelObject> (table: Table, condition: any, value: T): Promise<T>``

Runs an update query.

!!! note
    Same remark as ``select``.

### ``delete <T extends ModelObject> (table: Table, condition: any): Promise<T[]>``

Runs an delete query.

!!! note
    Same remark as ``select`` and ``update``.
