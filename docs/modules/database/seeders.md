# Seeders

You can create seeders if you want to create items automatically.

Let's create a file `post.ts` in the directory named `src/app/seeders`.

```ts title="./src/db/seeders/post.ts"
import { BaseSeeder } from "@fehujs/database"
import { Post } from "../../app/models/post"


export class PostSeeder extends BaseSeeder {
    readonly name = "create_initial_post"

    public async run() {
        await Post.create({
            id: Date.now(),
            title: "created by seeder",
            content: "this is a post created by the seeder"
        })
    }
}
```

Now, register the seeder (as for migrations, if your seeder is located in `./src/db/seeders`, it will be loaded automatically), otherwise:

```ts

// ...

const seeders: Record<string, BaseSeeder> = {
    ...await loadAndInstanciateSeeders(),
    "create_initial_post": new PostSeeder()
}
// ...
```

Then run `node fcli seeders create_initial_post`.

!!! note
    You __must__ specify the seeder key to run the seeder.
