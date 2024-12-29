# Reference

!!! tip
    You can see a demonstration about this by watching at the jeran ``run`` function implementation.

## ``buildAdditionalFiles``

Arguments: 

- ``dirPath``: string
- ``outDirPath``: string
- ``tsConfigPath``: string (default: "./tsconfig.json")

It permits to build files that could be imported dynamically by the main bundle.

## ``buildFiles``

Arguments:

- ``fileName``: string
- ``buildAdditional``: (file: string) => Promise<void> (not required)

It permits to bundle and build an endpoint (for example, a file in ``./bin/`` in a Fehujs app), the ``buildAdditional`` callback permits to execute others build depending on the file identifed.

## ``launchCommand(exec: string, args: string[])``

Runs a command using ``child_process.spawn()``. The ``exec`` argument is the name of the executable and the second argument represents the list of the others args.

## ``run``

This function is the endpoint of each Fehujs process. It's this function that identifies the ``./bin/`` file to bundle and then to run.
