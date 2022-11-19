## What is Version Control?
- Developers work on the same code
- Code is hosted centrally on the internet
- Every developer has the entire copy of the code locally
- Code is fetched from the remote repository and push back to remote repository when change is made
- Git know how to merge code automatically
- Merge Conflict: if the same line has been changed git can't fix it by itself, it should be dealt with manually. So pushing and pulling ofter important.
- Version Conrol keeps the history of the change in code, you can simply go back to previous version. Each change labeled with a commit message
- If you want to delete your local repo, you can simply delete .git file and the connection between the local repo and remote repo will be lost.

### Commands
- `git status` status of local git repo
- `git add .` changes goes from **working directory** to **stage**
- `git commit -m "[commit message]"` changes made in the local repository 
- `git push` changes is updated in the remote repository
- `git init` turning a folder into a local git repo by creating .git file inside the folder automatically
- `git branch` for checking if there is a new branch
- `git pull` for getting the changes and new branches locally
- `git checkout <branch name>` switching branch `git checkout master` switching to master branch
- `git checkout -b feature/database-connection` create and switch the new branch called feature/database-connection
- `git branch -d <branch name>` deletes branch

### Branches
- Best practice is a branch for each new feature and each new bug fix. (eg. feature/user-auth)
- After testing locally developers merge their branch to master branch
- when you create a new branch locally and want to push your change, you can simply type git push and git will suggest you to appropriate command for pusing your new branch

### Merge Request

### Deleting Branch
- Deleting the branch after merging is an option

### Git Rebase
- When we push a change to remote we may get an error that says remote repo is not up to date. Instead of git pull to sycn. we `can git pull -r` so there wouldn't be merge conflict.

