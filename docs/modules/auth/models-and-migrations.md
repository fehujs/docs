# Models & migrations

This module provides build-in migrations and models for users and auth tokens.

You can update them by making an inheritance.

!!! note
    The default provider for these models is ``SQLDatabaseProvider`` from the database module.
    You can update it by inheritance.

??? info "Default fields"

    The default user model contains: 

    - name
    - email
    - id
    - password 
    
    The default auth token model contains:
    
    - userId
    - token
    - expiration date
    - id

Now you can register these migrations in ./bin/migrate.ts`:

```ts hl_lines="5 6"
// ...

const migrations: Record<string, BaseMigration> = {
    ...(await loadAndInstanciateMigrations()),
    "add_user": new AddUserMigration(),
    "add_auth_token": new AddAuthTokenMigration(),
}
//...
```

Then run the migrations: `node fcli migrate add_auth_token=up add_users=up`.
