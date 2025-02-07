# init

The `init` action initializes the directory in which this command is called as a project directory and ties the directory to a certain Sandbox app. You can specify the application ID as an option; otherwise you are prompted to enter it.

Executing `init` within a project resets the project without deleting the extensions / themes.

## Options

Name | Description
--- | ---
`--appId` | The ID of the sandbox app to initialize.
`--force` | If used, the SDK does not require permission if you reset the project.

## Examples
```shell
sgconnect init
sgconnect init --appId shop_12345
sgconnect init --appId shop_12345 --force
```
