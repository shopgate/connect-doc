## Logger

Each step function has a context-aware logger available as `context.log`. The logger is based on the [Bunyan logger](https://github.com/trentm/node-bunyan). You can use it to log the following common log levels:

```javascript
context.log.trace(additionalDataObject, msg)
context.log.debug(additionalDataObject, msg)
context.log.info(additionalDataObject, msg)
context.log.warn(additionalDataObject, msg)
context.log.error(additionalDataObject, msg)
context.log.fatal(additionalDataObject, msg)
```

> In the production environment, the log level is set to info, meaning messages equal to or higher than info are logged. In the sandbox environment, the log level is set to debug.

> Please note that the Bunyan logger defines a set of core fields that are populated automatically. You cannot use these within additionalDataObject, because they will be overwritten. See the [list of core fields](https://github.com/trentm/node-bunyan#core-fields) in the Bunyan documentation for reference.
