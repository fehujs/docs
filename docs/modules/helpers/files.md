# File handling

## ``getFile(filename: string): Promise<Buffer<ArrayBufferLike>>``

Get the content of a file, depending on it's path.

## ``getFileFromTmp(filename: string): Promise<Buffer<ArrayBufferLike>>``

Get the content of a file stored in tmp storage.

## ``getFileFormat(filename: string): Promise<string>``

Get the format of a file depending on it's extension.

!!!note
    This function parses the file ``./src/content-types.json`` that contains a set of a lot of extensions with their content type.

    You can add as many as you want.

    If a file extension isn't registered in this set, the default is set to ``text/plain``.

## ``fileExists(filename: string): Promise<boolean>``

Check if a file exists.

## ``move(filepath: string, newPath: string, options: { overwrite: boolean } = { overwrite: false }): Promise<void>``

Moves the file `filepath` to a the `newPath` directory.

If `options.overwrite` is `true`, if a file A has the same name in the destination directory, A will be replaced by the other one. Otherwise, an error is raised.
