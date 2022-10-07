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
sudo adduser [User name]
sudo passwd [User name]
su [User name] : change to the user
su - : change to root user

sudo groupadd [group name]
sudo usermod -g devops tom : Tom is added to group devops
groups tom : shows all the groups that tom is a member

ls -l : shows the permission

sudo chown tom test.txt: tom becomes the owner of test file 

sudo chmod ( g+r g-w u+w u+x o-x o-w) [file name]

+ add
- remove

r:read
w:write
x:execute

u:user
g:group
o:other

sudo chmod g=rw- [file name}

4 read
2 write
1 execute
0 no permission

0 ---
1 --x
2 -w-
3 -wx
4 r--
5 r-x
6 rw-
7 rwx

sudo chmod 777 test.txt
