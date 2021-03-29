# Windows Terminal - Tips

![Banner](./banner.svg)

## Add new profile

Add a new profile to start Ubuntu and directly execute an interactive shell for a given container (let's say `myAppName`):

```json
{
    "profiles": {
        "list": [
            {
                "commandline": "wsl.exe -d Ubuntu docker-compose exec myAppName /bin/bash",
                "background": "#041f42",
                "tabColor": "#2496ED",
                "guid": "{YOUR_GUID}",
                "icon": "ms-appdata:///roaming/ubuntu.png",
                "name": "Docker - MyApp",
                "startingDirectory": "\\\\wsl$\\Ubuntu\\home\\repositories\\myAppProject"
            }
        ]
    }
}
```

Notes:

* `commandline`: to start a Linux subsystem, start your comand by `wsl.exe -d ` followed by the distribution name like `wsl.exe -d Debian` f.i. Of course, that distribution need to be on your machine. You can complete the command line by a parameter: the command to run on the startup like, f.i. `docker-compose` or `ls` or anything else.
* `guid`: To get a new GUID, run `uuidgen` in an Ubuntu shell. Then put the obtained value in your json here above (replace `YOUR_GUID` by the value).
* `ìcon`: In order to customize the icon, grab any icon from the Internet and save the image in the `%USERPROFILE%\AppData\Local\Packages\Microsoft.WindowsTerminalPreview_8wekyb3d8bbwe\RoamingState` folder.
