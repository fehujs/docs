# Models

Models are the objects that permit you to handle and store data during a request.

## Create a model

You need to create a directory named `src/app/models` and you create a new file containing your model in it.

Example: 

```ts title="post.ts"
import { BaseModel } from "@fehujs/database"

import { AddPostMigration } from "../../db/migrations/add_post"

export class Post extends BaseModel {
    public static table = (new AddPostMigration()).getTable()  // this is to avoid the rewriting of the table

    // if your (main) private key isn't 'id', change it there
    protected idCol: string = 'your_main_private_key_column_name'
    
    // don't forget to declare the fields in the model
    declare id: string

    declare title: string

    declare content: string
}
```

Please note that you can override every method of BaseModel if you need something more complex (you can see an example in the Auth module).

## Get

There's many ways to get datas from database with this system.

### ``Model.find(id: string | number): Promise<BaseModel>`` (static)

You can get an item with its primary key.

### ``Model.findBy(key: string, value: string, operator: Operator = '='): Promise<BaseModel[]>`` (static)

You can get many items using this function (key param stands for the column name, the value stands for the value to be compared, and the operator stands for the operation between key and the value)

### ``Model.findWithSql(condition: string): Promise<BaseModel[]>`` (static) (**depreciated**)

Supposed to return an array of models selected with a SQL selection, `condition`.

!!! danger "depreciated"
    Use instead `provider.query()` (returns an instance of Knex).

### ``Model.findAll(): Promise<BaseModel[]>`` (static)

Returns all items of a table.

## Create

### ``Model.create(options: ModelObject): Promise<BaseModel>`` (static)

Creates a new object in the database and returns it.

## Edit/save

### ``instance.save(): Promise<void>``

Let's have a demo:

```ts
    const post = new Post()
    post.id = "...."
    post.title = "hello there"
    post.content = "."

    // right now my model ("post") isn't stocked in the db

    post.save()

    // now it is

    post.content = "new content" // (1)!

    post.save() // (2)!
```

1. the update isn't stored in the db, but the new value is stocked in the model's data
2. the changes have been stocked in the db

## Delete

### ``instance.destroy(): Promise<void>``

Destroys the item specified.

## Format data

### ``instance.toObject(): ModelObject``

Returns the model data stocked in model.data, not the data from db (the difference is that the model.data may be different than db because it stores values updates before saving in the db).

### ``instance.toJson(): string``

Returns the model data stocked in model.data as JSON.

## Serializing

### ``instance.serialize(fields: Serialize): ModelObject | undefined``

Serializes the model according to provided fields.

This is the typing of fields:
```ts
type Serialize = {
    [keys: string]: {
        serializeAs?: string
        doSerialize?: (value: string | number) => string
    }
}
```

There's a little example:
```ts
const posts = await Post.findAll() as Post[]

const postsSerialized: ModelObject[] = await new Promise((resolve, reject) => {
    let serialized: ModelObject[] = []

    posts.forEach(async post => {
        const postSerialized = post.serialize({
            id: {
                serializeAs: "postId"
            },
            title: {
                doSerialize: (value: string | number) => `${value.toString().slice(0, 10)}...`
            }
        })
        serialized.push(postSerialized!)
    })
    
    resolve(serialized)
})
```
