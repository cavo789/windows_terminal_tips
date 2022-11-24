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

## Open multiple tabs during the startup process

Windows Terminal has a `startupActions` property which allows you to specify actions to be performed during the startup process.

Let's imagine I wish to launch two tabs; the default one (nothing to foresee) and a second tab. To make things easier to maintain, I'll use a profile:

```json
"startupActions": "; new-tab --profile \"DOS Command Prompt\"",
```

So now I need to create a profile called `DOS Command Prompt` :

```json
{
    "profiles": {
        "list": [
            {
                "backgroundImage": "c:/Users/christophe/backgrounds/xmens.jpg",
                "backgroundImageOpacity": 0.10000000000000001,
                "guid": "{0caa0dad-35be-5f56-a8ff-afceeeaa6101}",
                "hidden": false,
                "name": "DOS Command Prompt"
            },
        ]
    }
}
```

And hop, now by starting Windows Terminal, my default terminal will be opened (Ubuntu in my case) and, in a second tab, I'll also open a DOS console.

My profile can be quite complex:

```json
{
    "profiles": {
        "list": [
            {
                "backgroundImage": "c:/Users/christophe/backgrounds/MyProject1.jpg",
                "backgroundImageOpacity": 0.5,
                "commandline": "wsl.exe -d Ubuntu-20.04",
                "cursorColor": "#FFFFFF",
                "guid": "{1de7a17d-42f5-47b6-8196-e48706bf24a7}",
                "hidden": false,
                "icon": "ms-appdata:///roaming/ubuntu.png",
                "name": "MyProject1",
                "startingDirectory": "\\\\wsl$\\Ubuntu-20.04\\home\\christophe\\repositories\\crescendo2\\federaldatamanager",
                "tabTitle": "MyProject1"
            },
        ]
    }
}
```

And I can have multiple projects and multiple tabs:

```json
"startupActions": "; new-tab --profile \"MyProjject1\" ; new-tab --profile \"MyProjject2\" ; new-tab --profile \"MyProjject3\" ; new-tab --profile \"MyProjject4\" ",
```
