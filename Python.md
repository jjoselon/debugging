# How to debug python files on vs-code

1. Install [python extension](https://marketplace.visualstudio.com/items?itemName=ms-python.python)
2. Make sure you selected right **python interpreter path** in ">Select interpreter" section typing 'Ctrl+Shitp+P' in vs-code
3. Create the `launch.json` configuration file in your workspace folder and override contents with this
```json
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        
        {
            "name": "Python: Current File (Integrated Terminal)",
            "type": "python",
            "request": "launch",
            "program": "${file}",
            "console": "integratedTerminal",
            "args": [ // Example arguments (delete if you want)
                "-i", "420",
                "-t", "2020"
            ],
        },
        {
            "name": "Python: Remote Attach",
            "type": "python",
            "request": "attach",
            "port": 5678,
            "host": "localhost",
            "pathMappings": [
                {
                    "localRoot": "${workspaceFolder}",
                    "remoteRoot": "."
                }
            ]
        },
        {
            "name": "Python: Module",
            "type": "python",
            "request": "launch",
            "module": "enter-your-module-name-here",
            "console": "integratedTerminal"
        },
        {
            "name": "Python: Django",
            "type": "python",
            "request": "launch",
            "program": "${workspaceFolder}/manage.py",
            "console": "integratedTerminal",
            "args": [
                "runserver",
                "--noreload",
                "--nothreading"
            ],
            "django": true
        },
        {
            "name": "Python: Flask",
            "type": "python",
            "request": "launch",
            "module": "flask",
            "env": {
                "FLASK_APP": "app.py"
            },
            "args": [
                "run",
                "--no-debugger",
                "--no-reload"
            ],
            "jinja": true
        },
        {
            "name": "Python: Current File (External Terminal)",
            "type": "python",
            "request": "launch",
            "program": "${file}",
            "console": "externalTerminal"
        }
    ]
}
```
4. Open your python file and set the breakpoints you wish
5. Press F5 in vs-code to start debugging selecting `Python: Current File (Integrated Terminal)` action
