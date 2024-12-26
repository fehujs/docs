# Id generation

## ``randomId(prefix?: string): string``

It uses [paralleldrive/cuid2](https://npmjs.com/package/@paralleldrive/cuid2) under the hood.

If ``prefix`` is set, it will return ``"<prefix>_<id>``, otherwise it will return only the generated id.
