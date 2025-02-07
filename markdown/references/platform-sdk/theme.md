# theme

## upload

```shell
sgconnect theme upload [theme-directory]
```

This command uploads a theme to the Shopgate Developer Center.

`theme-directory` specifies the directory name of the theme to upload. If `theme-directory` is not specified, a list of all themes from the themes directory will be shown, and the user can select one of them.

The selected theme directory is packed into a TAR archive and uploaded to the Shopgate Developer Center.

If the version of the uploaded theme does not exist in the Shopgate Developer Center, a prompt is shown, asking if the version should be created automatically. If `--force` or `-f` option is specified, the version is created without prompting.

If the version is already uploaded and pushed into the status “Waiting for review,” a prompt will be shown to confirm the review request should be canceled. To force the canceling, set the option if `--force` or `-f`.

### Options

Name | Description
--- | ---
`-f`<br>`--force`|Force "yes" as answer to all prompts
`-t`<br>`--preprocess-timeout <ms>`|Specify preprocessing timeout in milliseconds (default: 60000)

### Examples

```shell
sgconnect theme upload
sgconnect theme upload myAwesomeTheme
sgconnect theme upload myAwesomeTheme --force
```
