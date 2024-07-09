----
# Something weird with paths in registry after the menu options get created (at least when installing with --user). 
# Doesn't get fixed running the `.reg` file, and icons were missing and path was messed up. Might need to fix this later or just manually work around it.
- Install path is `Computer\HKEY_CURRENT_USER\SOFTWARE\Classes\Directory\background\shell\(FOLDERS)`.
- Had to manually edit the path for icon and cmd at registry key path since it was missing `\` between directories.
- To remove other entries, for example if you are only using mingw64, just delete their folders at reg key path. This is also how you can uninstall the shell entries.
----
----

This implementation should work for MSYS2 and MINGW32/64 shells that come with MSYS2.

# <ins>Right click "Bash-here" Shortcut in Context Menu for MSYS2 MINGW32/64 shell
This is all the configuration files needed for adding "bash here" options in 
the Windows right-click shortcut/context menu.</ins>

![screenshot](https://cloud.githubusercontent.com/assets/2238599/15538737/d9d1e3a2-2232-11e6-9426-42c62c69925c.png)


## Usage
0. Make sure environment variable `%HOME%` exists. 
   (This script will source `%HOME%/.bash_profile`)
1. `git clone git@github.com:njzhangyifei/msys2-mingw-shortcut-menus.git` into
   your desired directory to install
   - Or `git clone https://github.com/njzhangyifei/msys2-mingw-shortcut-menus.git`
   when git via ssh is not available
2. `./install` and follow the instructions. Use `./install --user` for current user only
3. double-click `install_right_click_menu.reg` file to merge it into your
   windows registry
4. **(Optional)** If you don't see icons in the context menu, please install `msys2-launcher`
   via pacman (`pacman -S msys/msys2-launcher-git`) or from source https://github.com/elieux/msys2-launcher


## Note (TL;DR)
- This script does NOT depend on `cygpath`.
- If you are using Zsh, please copy-and-edit a `msys2_shell_zsh.cmd` in your
   MSYS2 install directory. You will also need to change `TEMPLATE_SHELL` in the
   install script to `zsh`. For example template, please see 
   `reg_aio_zsh_msys2_shell_example.template`.
- If you are using msys2 with filesystem newer than 2016.05-2, this script will
   only generate one `.reg` file. That's **ALL** you need to create this context
   menu. You can delete this directory after merging the `.reg` file.

### Note (For msys2 version with start_shell.cmd)
- For the MSYS2 version with `start_shell.cmd`, the script will 
  use `bash_here_start_shell.template` for generating bash scripts.
  - You **MUST** have environmental variable `$HOME` defined as 
    your home directory path.
- To use shell other than `bash` (e.g. to use `zsh`), you might want to create a 
  `start_shell_zsh.cmd` and `(mingw*/msys2)_shell_zsh.bat`. Then, you will need
  to modify either the template or the bash script generated to call the
  corresponding batch file.

## License
The MIT License (MIT) 2015 Yifei Zhang
