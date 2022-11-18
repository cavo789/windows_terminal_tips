# Windows Terminal - Tips

![Banner](./banner.svg)

## Installation

Is part of Windows 11 so should be available directly on your machine if you're running that OS.

You can install Windows Terminal using the Windows Store but, if you can't, you can download [the latest release from GitHub](https://github.com/microsoft/terminal/releases).

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

* `commandline`: to start a Linux subsystem, start your comand by `wsl.exe -d` followed by the distribution name like `wsl.exe -d Debian` f.i. Of course, that distribution need to be on your machine. You can complete the command line by a parameter: the command to run on the startup like, f.i. `docker-compose` or `ls` or anything else.
* `guid`: To get a new GUID, run `uuidgen` in an Ubuntu shell. Then put the obtained value in your json here above (replace `YOUR_GUID` by the value).
* `ìcon`: In order to customize the icon, grab any icon from the Internet and save the image in the `%USERPROFILE%\AppData\Local\Packages\Microsoft.WindowsTerminalPreview_8wekyb3d8bbwe\RoamingState` folder.

## Set the default profile

Take a look the list of profiles defined in your `settings.json` file, each profile has his own `guid`. Just copy/paste the guid of the profile of your choice to the `defaultProfile` root node.

## Set the default folder for Ubuntu

Directly open the desired directory is done by setting the `startingDirectory` node in a profile. Let's say we wish to open the user home folder by starting a new Ubuntu shell:

```json
{
  "profiles": {
    "list": [
      {
        "name": "Ubuntu",
        "source": "Windows.Terminal.Wsl",
        "startingDirectory": "\\\\wsl$\\Ubuntu\\home\\christophe\\"
      }
    ]
  }
}
```

You just need to specify the `startingDirectory` node and set it to `\\wsl$\Ubuntu\home\christophe\`
