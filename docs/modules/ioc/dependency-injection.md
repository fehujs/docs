# Dependency injection

If you want to use Dependency injection for your services, you can by defining your services in `src/app/services`:

```ts
import { Injectable } from "@fehujs/ioc"

@Injectable()
export class MyService extends BaseService {
    getData() {
        return { data: "my data" }
    }
}
```

The ``Injectable`` decorator permits to define a class that could be injected.

Then in your controller:

```ts
import { Inject } from "@fehujs/ioc"

export class TestDIController extends BaseController {
    constructor(@Inject(MyService) protected myService: MyService) {
        super()
    }

    myView({ response }: HttpContext) {
        return response.setResponse({
            body: JSON.stringify(this.myService.getData()),
            contentType: "application/json"
        })
    }
}
```

The ``Inject`` decorator defines a dependency of the class.

You can register the views like all controllers.

!!! tip
    You can inject services into services:

    ```ts
    @Injectable()
    export class SecondService extends BaseService {
        getData() {
            return "hello, world"
        }
    }

    @Injectable()
    export class FirstService extends BaseService {
        constructor(@Inject(SecondService) protected secondService: SecondService) {
            super()
        }

        getData() {
            return { data: this.secondService.getData() }
        }
    }
    ```

    And then in the controller:

    ```ts
    export class TestDIController extends BaseController {
        constructor(@Inject(FirstService) protected firstService: FirstService) {
            super()
        }

        myView({ response }: HttpContext) {
            return response.setResponse({
                body: JSON.stringify(this.firstService.getData()),
                contentType: "application/json"
            })
        }
    }
    ```

!!! tip
    You can inject as many services as you want.

    ```ts
    export class TestDIController extends BaseController {
        constructor(
            @Inject(FirstService) protected firstService: FirstService,
            @Inject(SecondService) protected secondService: SecondService,
        ) {
            super()
        }

        myView({ response }: HttpContext) {
            console.log(this.secondService.getData())

            return response.setResponse({
                body: JSON.stringify(this.firstService.getData()),
                contentType: "application/json"
            })
        }
    }
    ```
