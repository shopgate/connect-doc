# backend

The `backend` action starts the backend part of the SDK.


## start

```shell
sgconnect backend start
```

This command connects your local development environment to the Shopgate CONNECT platform and maintains this connection until you abort the command with Ctrl-C (or any terminating signal). While running, the command outputs status information and a debug log.

You can start this command in inspection mode by using the `--inspect` flag. This enables you to use your debugger to debug extension code. Refer to the Platform SDK Documentation for further information.

### Examples

```shell
sgconnect backend start
sgconnect backend start --inspect
```
