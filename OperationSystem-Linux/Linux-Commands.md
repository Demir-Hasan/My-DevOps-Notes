## Frequently Used Commands in Linux CLI


- `mkdir` python-projects : Creates a file named "python-projects"
- `touch` Readme.md
- `rm` Readme.md : removes the file
- `rm -r` python-projects : remove the directory and all the files in it. -r means recursive
- `cd /` : takes you to root folder
- `cd ../..` goes back two times
- `cp` Readme.md Text.md
- `ls -R` Documents: it shows all the folders in Documnets and its contents
- `Ctrl + r` = Search history
- `history 20` : shows the last 20 commands
- `cat` : shows the content of the file
- `cat /etc/os-release`
- `lscpu`
- `lsmem`

- `su -` [user]

- `mv Downloads/Docker-server.pem ~/.ssh/` moving the private key file from downloads folder to ssh folder
- `ssh -i ~/.ssh/docker-server.pem ec2-user@[Public IP address from AWS]` It connects us to AWS server as ec2 user
- `ps aux | grep docker` to check if docker is running


##Installing/Uninstalling App

- `sudo apt search` {the name of the software}
- `sudo apt install` the name of the software
- `sudo apt remove` the name of the software

----------------
VIM Text Editor
----------------
- `dd` : delete the line on which cursor is located
- `d10d` : delete the 10 line
- `u` : undo the changes
- `0` : jump to beginning of the line
- `A` : jump to the end of the text
- `$` : jump to end of the line
- `12G` : goes to line12
- `/` : search mode n: jumps to next match

----------------------------
User - Groups - Permissions
----------------------------
- sudo adduser [User name]
- sudo passwd [User name]
- su [User name] : change to the user
- su - : change to root user

- sudo groupadd [group name]
- sudo usermod -g devops tom : Tom is added to group devops
- groups tom : shows all the groups that tom is a member

- ls -l : shows the permission

- sudo chown tom test.txt: tom becomes the owner of test file 

- sudo chmod ( g+r g-w u+w u+x o-x o-w) [file name]

- + add
- - remove

- r:read
- w:write
- x:execute

- u:user
- g:group
- o:other

- sudo chmod g=rw- [file name}

- 4 read
- 2 write
- 1 execute
- 0 no permission

- 0 ---
- 1 --x
- 2 -w-
- 3 -wx
- 4 r--
- 5 r-x
- 6 rw-
- 7 rwx

- sudo chmod 777 test.txt

-----------------
Shell Scripting
-----------------

- When we want to execute a set of commands, we can do it by executing a file that that have all commands we want to execute. Since this is a file, it can be stored,
transferred, moved, and executable more than once.
- `#!/bin/sh` is called shebang. # : sharp ! : bang
- In the abc.sh file the first line should be `#!/bin/sh` Otherwise, the OS does not recognize it to run the file.
- To run the file we enter the following syntax to command line : `**./**abc.sh` or `**bash** abc.sh`
- `file_name=config.yaml` echo "using file $file_name to configure something." $ indicates variable.
- `variable_name = $(command)` : store output of a command in a variable. Example : confi

```
if [condition] 
then
  statement
else
  statement
 fi 
```

```
echo "all params : $*"
echo "number of params : $#"

for param in $*
  do 
    echo $param
  done
  
- we run the file ./abc.sh param1 param2 param3 ...  
  
```

----------------------
ENVIRONMENT VARIABLES
----------------------
- `printevn | less`
- `printenv USER`
- `printenv | grep USER`
- `echo $USER`
Setting an environment variable:
- `**export** DB_USERNAME = dbuser`

Deleting an environment variable
- `**unset** DB_USERNAME`

Persisting environment variables
- `vim .bashrc` we add our env variables in this file. 
- `source .bashrc` this command is like saving the changes or applying the changes. when we reopen the terminal changes will be there.

-----------
Networking Commands
---------------
- `ifconfig` network info of the machine
- `netstat` shows active connections
- `ps aux`
- `nslookup`
- `ping`

----------
Establishing a SSH connection
---------
- First we need to be able to connect to remote server by password. In order to do that we can use the command `SSH root@[remoter server IP` 
- `ssh-keygen -t rsa` to generate SSH key pair. 
- id_rsa: private key | id_rsa.pub: public key
- `cat id_rsa.pub` we copy all the data to the autorized_keys file in the remote server. 
- Once the connection is built we can access the remote server by `SSH -i .ssh/id_rsa root@IP` or if we have only 1 connection `SSH root@IP` is enough. 
- `scp` secure copy: this is used when we copy something from our machine to the remote server. for example: `scp test.sh root@IP:/root`
-  


