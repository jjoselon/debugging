# How to debug php apps from vs-code
1. Install [felixfbecker.php-debug](https://marketplace.visualstudio.com/items?itemName=felixfbecker.php-debug) extension
2. Run `php -i >> phpinfo.md` command to figure out php information.
3. Copy && Paste content in this form [https://xdebug.org/wizard](https://xdebug.org/wizard)
4. Wizard tell you xdebug version you have to install (or install yet)
5. Install xdebug in your OS (e.g on ubuntu sudo apt install php-xdebug) follow instructions version number that xdebug wizard recommend!
6. Replace Xdebug section config in `/etc/php/7.3/mods-available/xdebug.ini` or `php.ini` (if there are not, simple add config at the end of file) contents with:
```ini
; For Xdebug in general (I think)
zend_extension=xdebug.so
xdebug.remote_handler = dbgp
xdebug.remote_host = 127.0.0.1
xdebug.remote_log = /home/xdebug_remote.log
xdebug.remote_mode = req
xdebug.remote_port = 9005
xdebug.remote_connect_back = 1

; For Xdebug v3.x.x:
xdebug.mode = debug
xdebug.start_with_request = yes
xdebug.client_port = 9005

; For Xdebug v2.x.x:
xdebug.remote_enable = 1
xdebug.remote_autostart = 1
```
7. Restart fpm service and server (ngnix or apache) is required
8. Create the launch.json file in your workspace with this:
```json
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        
        {
            "name": "Listen for XDebug",
            "type": "php",
            "request": "launch",
            "port": 9005
        },
        {
            "name": "Launch currently open script",
            "type": "php",
            "request": "launch",
            "program": "${file}",
            "cwd": "${fileDirname}",
            "port": 9000
        }
    ]
}
```
9. Set breakpoints in your php file, press `F5` in vs-code (make sure you selected "Listen for XDebug" action, vs-code toolbar tell you)
10. XDebug listen requests and execute breakpoints configured
11. Enjoy!
