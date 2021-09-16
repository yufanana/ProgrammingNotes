# Linux Notes

Author: __*yufanana*__
</br>
____

## Table of Contents <a name="top"></a>
1. [File System](#1)<br>
2. [File Editing](#2)<br>
3. [Moving/Renaming Files](#3)<br>
4. [Bash Config Files](#4)<br>
5. [Permissions](#5)<br>
6. [Resources Usage](#6)<br>
7. [Manage Systemd Units](#7)<br>
8. [View Logs](#8)<br>
9. [Manage Users](#9)<br>
10. [Bash History](#10)<br>
11. [Output Redirection](#11)<br>
12. [Streams](#12)<br>
13. [Variables](#13)<br>
14. [Find](#14)<br>
15. [OpenSSH](#15)<br>

## 1 File System<a name="1"></a>
[Go to top](#top)

- `ls` list storage: views all the items in the working directory
- `ls /`:  shows the root file system
- `ls -l /` long listing: to view the items in details, or `ll`
- `ls -a` shows all the files, including the hidden files

- `pwd` print working directory
- `~`: shorthand for the home directory
- `*.txt` refers to all the .txt files
- `..` refers to the parent directory
- `.` refers to the current directory
- `!!` reruns the latest command

- `which nano` shows the directory of the program of the specified application

files with a . prefix are hidden.

Directory Structure
- `home`: contains a folder for each user, personal files. 
- `bin`: binary, executable programs
- `boot`: contains files needed to boot the system, bootloader <
- `etc`: contains configuration files
- `opt`: contains optional software packages
- `root`: home directory of the root user 
- `usr`: contains applications & files user by users

## File Editing<a name="2"></a>
[Go to top](#top)

- `touch myFile.txt` create file: create the specified file if it does not exist
- `nano`: uses the nano text editor
    - `nano myFile2.txt` to edit (and create) the specified file
- `cat myFile.txt` displays the content of the specified file
- `vim myFile.txt` uses the vim text editor

## Moving / Renaming Files<a name="3"></a>
[Go to top](#top)

- `cp fileName.txt destination.txt` copy: copy the specified file into the destination file
- `diff file1.txt file2.txt` checks whether the files are different
- `rm file.txt` removes the specified file
- `mkdir myDirectory` makes a new directory
- `mv file.txt myDirectory` moves the specified file to the specified folder/directory
- `mv myFile.txt newName.txt` renames the file to the new file name

## Bash Configuration File<a name="4"></a>
[Go to top](#top)

When a terminal is opened, it will read the .bashrc file and load the settings/configuration written in the file.

- `nano /etc/skel/.bashrc/` contains the default bashrc file
- `nano .bashrc`

Aliases can be created as shorthand notations to save typing.
- `alias` displays all the aliases used in the terminal
- `unalias myAlias` removes the alias for the current session only (?) 

## Permissions<a name="5"></a>
[Go to top](#top)

`ls -lhd --time-style=long-iso --color=auto`

`drwxrwxr-x` has 4 sections
1. `d`: directory (d) or file (-)
2. `rwx`: user (owner of file or directory)
3. `rwx`: group
4. `r-x`: other/world

- `r` read permission (4)
- `w` write, modify (2)
- `x` execute (1)

- `chmod +x myScript.sh` change mode: add the specified permission to the specified file/directory for all
- `chmod u+x myScript.sh` to give permission to USER
- `chmod a+rwx myScript.sh` to give permission to all
- `chmod -x myScript.sh`
- `chmod 400 myFile.txt` to change permissions to User:4, Group:0, Others:0, so `-r--------`
- `chmod 647 myFile.txt` to change permissions to User:rw, Group:r, Others:rwx

For directories,
- `r` able to see contents
- `w` able to change contents
- `x` able to enter into directory

## Resource Usage<a name="6"></a>
[Go to top](#top)

- `free -m` shows available memory in megabytes
- `df -h` disk free, human-readable
- `df -i` shows inodes

## Managing Systemd Units<a name="7"></a>
[Go to top](#top)

Check service, application, etc, running in the background.

- `sudo systemctl status apache2` to check the status of the specified application/software

- `sudo systemctl disable apache2` to not run the software everytime the machine starts
- `sudo systemctl enable apache2` to run the software everytime the machine starts

- `sudo systemctl stop apache2` to terminate the specified software
- `sudo systemctl start apache2` to run the software for the current session
- `sudo systemctl restart apache2` if the configuration had changed

## Viewing Logs<a name="8"></a>
[Go to top](#top)

To understand what went wrong in the system

- e.g. `cat /var/log/syslog`
- `~ dmesg`
- `head cat /var/log/syslog` shows the first 10 lines of the log
- `tail cat /var/log/syslog` shows the last 10 lines of the log

- `tail -n 50 cat /var/log/syslog` shows the last 50 lines of the log
- `tail -f /var/log/syslog` follows the last 10 lines of log file, updates live

- `journalctl -u apache2` shows the log messages related to specified software
- `journalctl -fu apache2` follows the log messages related to specified software

## Managing Users<a name="9"></a>
[Go to top](#top)

- `cat /etc/passwd` shows all the users
- `cat /etc/group` shows all the groups or `groups`
- `sudo adduser newUser`
- `passwd` to change password
- `su - anotherUser`

## Bash History<a name="10"></a>
[Go to top](#top)

- `history` displays the bash history with the command numbers
- `!594` will re-execute the specified command
- Adding a space in front of the command will hide it from the history

## Output Redirection<a name="11"></a>
[Go to top](#top)

- `ls -l > file.txt` redirects (writes over) output from the command into the file
- `ls -l >> file.txt` redirects (append) output from the command into the file

- `ls -l | grep file` chains the command by taking the output from the first command as input to the next command. "piping"

## Streams<a name="12"></a>
[Go to top](#top)

standard input (0), standard output (1), standard error (2)

- `echo $?` outputs return value of previous command
- `find / -name *.log 2 > error.txt` redirect error log messages into error.txt file

## Variables<a name="13"></a>
[Go to top](#top)

- `echo "my string"` echo returns anything contained in quotation marks

Variables created are specific to the session.
- `HELLOMSG="Hello World"` creates a variable
- `MR_DIR="/etc/"` 
- `echo $HELLOMSG` returns the content of the variable
- `env` shows all the variables available (beyond the shell session)
- `export MY_VAR="4"` adds the variable to the env

## Find<a name="14"></a>
[Go to top](#top)

- `find  -name log` find anything with log inside
    - `-type f` or `-type d` search for file or directory
    - `-name` search by name 
    - `/var` to search in the specified directory
    - `*"log*"` 
    - `-mtime -7` search for files with modified time within last 7 days
    - `-exec rm {} \;` run the executable command, that is to remove anything found
- `find / -name *.log 2 > error.txt` redirect error log messages into error.txt file

## OpenSSH<a name="15"></a>
[Go to top](#top)

- `sudo apt install openssh-server` to install SSH
- `sudo netstat -tulpn` or `which sshd`
- `ip a` to obtain the IP address
- `ssh user@<IP>` log into the specified user at the specified IP address
