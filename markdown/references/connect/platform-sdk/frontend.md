# frontend

You use the `frontend` actions to set up and start the frontend development server, which makes it easier to develop and test frontend code locally.

## setup

```shell
sgconnect frontend setup
```

This command runs the set up wizard, which includes the following questions:

1. **Which IP address should the app connect to?**  
The IP address should be your local IP address. You can either use `127.0.0.1` to point to you local machine or use another IP address that is reachable in your local area network.

2. **On which port should the app run?**  
The development server uses a Webpack development server which requires a port to run. This port is part of the URL you open in the browser later. The default port is `8080`.

3. **On which port should the Rapid API run?**  
The development app makes pipeline requests to a mock server on your local machine, so you must set a port that the requests will be sent to. The default port is `9666`.

4. **On which port should the HMR (Hot Module Replacement) run?**  
When developing with Webpack, you can take advantage of [Hot Module Replacement](https://webpack.js.org/concepts/hot-module-replacement/) (HMR). The server instantiates a WebSocket to listen for changes to the project files. This socket requires a port to listen to. The default port is 3000.

5. **On which port should the remote dev server (redux) run?**  
To debug changes in your testing app on your device, you can look at the Redux store. To do this, start the development server with the remote dev server for redux enabled. This remote server also requires a port to pass information through. The default port is `8000`.

6. **Please specify your development sourcemap type**  
By default, the source maps type is set to cheap-module-eval-source-map. You can change this setting for your local development environment. Refer to the official [webpack documentation](https://webpack.js.org/configuration/devtool/) for a list of the possible types.

7. **Are these settings correct?**  
You can check if all of your settings are correct.

The command saves your configuration. You can re-run this command again at any time to change the settings.

## start

```shell
sgconnect frontend start
```

This command starts the development server. If you have more than one theme in your project, this command provides a list of the themes. You must select which theme to use. This list does not display if you choose to use the `--theme` option instead.

### Options

Name | Description
--- | ---
`--theme, -t` | The theme that will be compiled by Webpack.
`--host, -h` | Webpack automatically uses your configured IP address as its host address. With this option, you can temporarily change the host to something else. For example, you could set it to `http://localhost`.
`--port, -p` | You can temporarily change the port of your development server.
`--analyze, -a` | Specifies whether to analyze the bundle sizes.

### Examples

```shell 
sgconnect frontend start
sgconnect frontend start --theme {your-theme}
sgconnect frontend start --host {your-new-host}
sgconnect frontend start --port {your-new-port}
sgconnect frontend start --analyze
```
