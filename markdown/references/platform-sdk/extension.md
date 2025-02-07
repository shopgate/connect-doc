# extension

You can use the `extension` actions to create new extensions and manage extension status within your application folder. 

## create

```shell
sgconnect extension create [types...]
```

This command creates a new extension folder inside your application folder and clones the Shopgate extension boilerplate repository into it. The new extension folder contains basic folder structure and getting started files.

You can specify one or more types (such as `backend` and `frontend`) to include specific folders and files for these specific areas of development.

### Options

Name | Description
--- | ---
`--extension [name]` | The name of the extension to create.
`--trusted` | Specifies whether to make this extension trusted; you can add a parameter value (true|false) to explicitly specify if the extension is trusted or not; the explicit expression is deprecated.


### Examples

```shell
sgconnect extension create --extension myAwesomeExtension
sgconnect extension create --extension myAwesomeExtension --trusted
sgconnect extension create --extension myAwesomeExtension --trusted false
sgconnect extension create --extension myAwesomeExtension --trusted false frontend
sgconnect extension create --extension myAwesomeExtension --trusted false backend
```

## attach / detach

```shell
sgconnect extension attach [{extension-name}...]
sgconnect extension detach [{extension-name}...]
```

This command attaches or detaches the specified extensions (or all locally available extensions if no extension names are specified).

When you attach an extension, all extension steps execute locally if they are included in any pipeline called by the frontend. Changes by this command will only take effect after you (re)start the frontend and/or backend process.

### Examples

```shell
sgconnect extension attach
sgconnect extension attach myAwesomeExtension
sgconnect extension attach myAwesomeExtension myMuchMoreAwesomeExtension
sgconnect extension detach
sgconnect extension detach myAwesomeExtension
```

## manage

```shell
sgconnect extension manage
```

The manage command provides a list of available extensions and their current attachment status. You can select or unselect extensions to change their attachment status.

## upload

```shell
sgconnect extension upload [extension-directory]
```

This command uploads an extension to the Shopgate Developer Center.

`extension-directory` specifies the directory name of the extension to upload. If `extension-directory` is not specified, a list of all available extensions is shown, and the user can select one of them.

The selected extension directory is packed into a TAR archive and uploaded to the Shopgate Developer Center.

If the version of the uploaded extension does not exist in the Shopgate Developer Center, a prompt is shown, asking if the version should be created automatically. If `--force` or `-f` option is specified, the version is created without prompting.

If the version is already uploaded and pushed into the status “Waiting for review,” a prompt will be shown to confirm the review request should be canceled. To force the canceling, set the option if `--force` or `-f`.

### Options

Name | Description
--- | ---
`-f`<br>`--force`|Force "yes" as answer to all prompts
`-t`<br>`--preprocess-timeout <ms>`|Specify preprocessing timeout in milliseconds (default: 60000)

### Examples

```shell
sgconnect extension upload
sgconnect extension upload myAwesomeExtension
sgconnect extension upload myAwesomeExtension --force
```
