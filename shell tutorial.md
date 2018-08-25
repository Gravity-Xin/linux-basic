# Linux Shell Tutorial

## Several Common Shells

- BASH Bourne-Again Shell
- CSH C Shell
- KSH korn Shell
- TCSH Enhanced and Compatible of CSH

use `cat /etc/shells`  to list shells on platform
use `echo $SHELL` to find out current shell type
use `ps $$` to find out current shell process

user <-> shell <-> kernel

## Basic Shell Line Editing

- Ctrl+L clear the screen
- Ctrl+W clear the word from start to cursor
- Ctrl+U clear the line
- Up/Down recall history commands
- Tab auto-complete
- Ctrl+R search history commands
- Ctrl+C cancel current running command
- Ctrl+T swap the last two characters before the cursor
- ESC+T swap the last two words before the cursor

## Shell Commnds

- Internal commands: builtins, part of the shell itself
- External commands: separate binary stores in /sbin, /usr/sbin, /usr/bin, /bin, /usr/local/bin

use `type cmd` to find out whether a cmd is a builtin or a external binary

the BASH shell understand the flowing types of command:

- Aliases: such as ll
- Keywords: such as if
- Functions: user defined functions
- Builtin: such as pwd
- Binary Files: such /usr/bin/date

## Login/out and BASH

when user login and logout, bash use the following initialization, startup and cleanup files

- /etc/profile: systemwide init file
- /etc/bash.bashrc: systemwide per-interactive-shell startup file
- /etc/bash.logout: systemwide logout cleanup file
- $HOME/.bash_profile: user init file
- $HOME/.bashrc: user per-interactive startup file
- $HOME/.bash_logout: user logout cleanup file
- $HOME/.inputrc: user readline init file