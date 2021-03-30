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

## Install zsh and oh-my-zsh

1. First, install zsh like this: `sudo apt install zsh`.
2. Then set zsh as your default shell: `chsh -s /usr/bin/zsh`
3. This done, install oh-my-zsh: `sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"`

### Install plugins

Note: each time a plugin has to be activated, you'll need to edit the `~/.zshrc` file and add his name to the list of plugins to load.

Edit the file and search for the `plugins=( ... )` array. Add the plugin name to the list. Save the file and the plugin will be loaded the next time you'll create a session.

#### zsh-autosuggestions

> [https://github.com/zsh-users/zsh-autosuggestions/blob/master/INSTALL.md#oh-my-zsh](https://github.com/zsh-users/zsh-autosuggestions/blob/master/INSTALL.md#oh-my-zsh)

This plugin will predict your command based on your history (a command you've already typed in) or, for instance, you're typing `cd ` and the plugin will automatically suggest the list of folders in the current directory. You're typing `cat ` and you'll get this time a list of file names.

Absolutely essential.

```bash
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

#### zsh-syntax-highlighting

> [https://github.com/zsh-users/zsh-syntax-highlighting/blob/master/INSTALL.md](https://github.com/zsh-users/zsh-syntax-highlighting/blob/master/INSTALL.md)

Provide highlighting in the prompt. Practical

```bash
git clone https://github.com/zsh-users/zsh-syntax-highlighting ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

#### fzf - Command-line fuzzy finder

> [https://github.com/junegunn/fzf](https://github.com/junegunn/fzf)

Usage

* Press <kbd>CTRL</kbd>-<kbd>R</kbd> and get a prompt with your history.
* Get the full list of files under the current folder by typing `fzf` and get a list of files; press enter and the filename is selected.
* Use the `|` (pipe) to filter on a filename, interactively
* and much more, take a look to the video tutorial: [https://www.youtube.com/watch?v=qgG5Jhi_Els](https://www.youtube.com/watch?v=qgG5Jhi_Els)

```bash
git clone --depth 1 https://github.com/junegunn/fzf.git ~/.fzf ; ~/.fzf/install
``` 


## Install the powerlevel10k theme

> [https://github.com/romkatv/powerlevel10k](https://github.com/romkatv/powerlevel10k)

Installation is made of four steps.

### Get the powerlevel10k theme

```bash
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
```

### Set powerlevel10k as default theme

This done, edit the `~/.zshrc` file and update the `ZSH_THEME` like this: 

```ini
ZSH_THEME="powerlevel10k/powerlevel10k"
```

### Install powerlevel10k fonts

Donwload the four fonts from [https://github.com/romkatv/powerlevel10k#manual-font-installation](https://github.com/romkatv/powerlevel10k#manual-font-installation): download one by one and click on the download file. Windows will open it and you'll get a windows with an `Install` button.

This done, open the Windows Terminal settings and open the `settings.json` file. Add the `MesloLGS NF` font in the `defaults` section for `profiles`, like this:

```json
{
  "profiles": {
    "defaults": {
      "fontFace": "MesloLGS NF"
    }
  }
}
```

### Configure powerlevel10k

Once the `~/.zshrc` file has been updated and fonts installed, just create a new Linux session. The `powerlevel10k` configuration script will be started and if everything is going fine, you'll see the correct symbol (if not, fonts were incorrectly installed).

Follow the wizard and make your choice in the different options.

If you want to display the username in the prompt, follow this [guide](https://gitee.com/kongren/powerlevel10k#how-do-i-add-username-andor-hostname-to-prompt).
