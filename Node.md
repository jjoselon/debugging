[https://code.visualstudio.com/docs/editor/debugging](https://code.visualstudio.com/docs/editor/debugging)
[https://code.visualstudio.com/docs/nodejs/nodejs-debugging#_attaching-to-nodejs](https://code.visualstudio.com/docs/nodejs/nodejs-debugging#_attaching-to-nodejs)
# How debug node apps using Visual Studio Code

1. Create an **attach** configuration in `launch.json` configuration file

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "type": "node",
            "request": "attach",
            "name": "Attach request",
            "cwd": "${workspaceFolder}/node_server.js"
        },
        {
            "type": "node",
            "request": "launch",
            "name": "Launch Program resquest",
            "program": "${workspaceFolder}/node_server.js"
        }
    ]
}
```
2. Run javascript file witn `node` adding **`--inspect`** option (required to debugging)

```console
node --inspect node_server.js [argumenst...]
```
3. Press `F5` in script to start debugging (Make sure you selected **Attach request** action in vs)
4. Request route (e.g /login) to enable breakpoints configured
