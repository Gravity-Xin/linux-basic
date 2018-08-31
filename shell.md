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
  
        | System Varible | Meaning                                                |
        | :------------: | :----------------------------------------------------: |
        | BASH_VERSION   | the version of this bash                               |
        | HOSTNAME       | the name of this computer                              |
        | CDPATH         | the search path of cd cmd                              |
        | HISTFILE       | the name of the file in which save the history command |
        | HISTFILESIZE   | the maximum number of commands in history file         |
        | HISTSIZE       | the number of commands in history file                 |
        | HOME           | the home dir of current user                           |
        | PATH           | the search path for commands                           |
        | SHELL          | path to login shell                                    |

  - user defined variables
    - created and maintained by user
  - use `echo "$vareName"` or `echo ${varName}` to view the variable value
  - use `varName=someValue` to assign
  - use `unset varName` to delete variables or functions
  - default shell var value
    - `echo ${var=value}`, if var is not set, then set var to value
    - `echo ${var:=value}`, if var is empty, then set var to value
  - rules for var name
    - begin with alpha or underscore
    - do not push space on either side  of equal sign
    - var name are case sensitive
    - user `varName=` or `varName=""` to define NULL variable
  - we can use wildcards in shell, such as `echo /etc/*.conf`  
- quoting in shell: tell shell to stop expanding
  
    | Quote Type   | Meaning                                                                                     | example                                                    |
    | :----------: | :-----------------------------------------------------------------------------------------: | :--------------------------------------------------------: |
    | doule quote  | protect everything enclosed except $ ' ", Varible:Yes Wildcards:No Command Substitution:Yes | `echo "$SHELL" echo "/etc/*.conf" echo "today is $(date)"` |
    | single quote | protect everything enclose, Varible:No Wildcards:No Command Substitution:NO                 | `echo '$SHELL' echo '/etc/*.conf' echo 'today is $(date)'` |
    | backslash    | change the special meaning of characters or to escape                                       | `echo "Path is \$PATH" echo "Path is $PATH"`               |
  
  - use backslash as the last character on line to contine command on the next line
- use export builtin to exports the variables or function of child process, by default all user defined variables and functions are local
- use env to view all environment variables, which will be passed to child process
- use read builtin to accept input from keyboard and assign it to variables
  - basic usage: `read -p "Prompt" var1 var2 var3`
  - timeout: `read -t 10 -p "this read cmd will timeout within 10 seconds" var1 var2`
  - password: `read -s -p "enter your password" var1`
- perform arithmetic opertions
  - arithmetic expansion: `$((n1+n2))`
  - use expr or bc command
- use declare bultin to create integer variable: `declare -i varName=10`
- user readonly or declare built to create consts: `readonly varName=value` or `declare -r varName=value`
  - read only variable can not be unset
- variable existence check
  - `${varName?this script will stop executing if varName is not defined}`
  - `${varName:?this script winn stop executing if varName is not defined or is empty}`
- use history builtin to  display a list of command you entered at a shell prompt
  - use `!!` to repeat the last command
  - use `!10` to repeat the command which line number is 10
- path name expansion
  - curly braces: `echo i like {tom, jerry}`, `echo file{1, 2, 3}.txt`
  - wildcards: `ls /etc/*.conf`
  - combine: `ls *.{c, h}`
- create and use aliases
  - use `alias` to display list of defined aliases
  - add user defined aliases to ~/.bashrc file
  - use `alias name='command'` or `alias name = 'command arg1 arg2'` to create alias
  - use `unalias name` to remove alias
- the tilde expansion: the `~` may be used to refer your home dir
- shell init file execution order
  - /etc/profile runs first, act as a system wide profile for bash shell
  - /etc/profile.d is called by /etc/profile, it runs second when a user login
  - ~/.bash_profile is runs third when user login, this file calls ~/.bashrc
- shell init file usage
  - set PATH and PS1(shell prompt)
  - set default printer via PRINTER
  - set default text editor via EDITOR
  - set default pager via PAGER
  - set default unmask
  - set up aliases
  - set up functions
- conditional execution
  - test builtin is used to check file types and compare value: `test condition && true-command || false-command`
  - use if statement to test a condition
    ``` shell
    if condition
    then
        command1
        command2
    else
        command3
        command4
    if
    ```

    ``` shell
    if test var == value
    then
        command1
        command2
    else
        command3
        command4
    if
    ```

    ``` shell
    if [ condition ]
    then
        command1
        command2
    else
        command3
        command4
    if
    ```
    - the if statement can be nested
    - use `if then elif then else fi` to create multilevel if statement
  - the exit status of a command
    - use `echo $?` to get the exit status of previous command
    - use `varName = $?` to store the exit status of previous command
  - logic And: && run second command only if the first command is successful
  - logic OR: || run second command only if the first command is not successful
  - you can combine both logic operators: cmd1 && cmd2 || cmd3
  - logic Not: ! used to test whether expression is true or not `if test ! condition`
  - beside test, you can also use [] to check file types and compare values
  - bath test and [] supports:
    - file attribute comparsion:
    - string comparsion:
    - arithmetic comparsion:
