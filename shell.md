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

## Shell Commnd Types

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

## Write Shell Script

- start a shell with `#! /bin/bash`: it indicate an interpreter for execution of this shell
- shell comments: `# comments`
- execute a script: `chmod +x script.sh; ./script.sh` or `bash script.sh`
- debug a script:
  - use `bash -xv script.sh`
  - use shell builtin set command:
    - set -x: display commands and their arguments as they are executed
    - set -v: display shell input lines as they are read
    - set -n: read commands but do not execute them
- variables in shell:  
  - system variables:
    - created and maintained by shell itself
    - use `set` or `env` or `printenv` to show all system variables
    - commonly used system varible
  
        |System Varible    |             Meaning                                  |
        |:----------------:|:----------------------------------------------------:|
        |BASH_VERSION      |the version of this bash                              |
        |HOSTNAME          |the name of this computer                             |
        |CDPATH            |the search path of cd cmd                             |
        |HISTFILE          |the name of the file in which save the history command|
        |HISTFILESIZE      |the maximum number of commands in history file        |  
        |HISTSIZE          |the number of commands in history file                |
        |HOME              |the home dir of current user                          |
        |PATH              |the search path for commands                          |
        |SHELL             |path to login shell                                   |
  - user defined variables
    - created and maintained by user
  - use `echo "$vareName"` or `echo ${varName}` to view the variable value
  - use `varName=someValue` to assign
  - 