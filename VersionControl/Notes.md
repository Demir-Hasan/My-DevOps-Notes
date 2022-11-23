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
- `git rm -r --cached <file name>` (gitignore) to update the remote repo by deleting the files

### Branches
- Best practice is a branch for each new feature and each new bug fix. (eg. feature/user-auth)
- After testing locally developers merge their branch to master branch
- when you create a new branch locally and want to push your change, you can simply type git push and git will suggest you to appropriate command for pusing your new branch

### Merge Request

### Deleting Branch
- Deleting the branch after merging is an option

### Git Rebase
- When we push a change to remote we may get an error that says remote repo is not up to date. Instead of git pull to sycn. we `can git pull -r` so there wouldn't be merge conflict.

### Git Ignore
- .gitignore (Don't track certain files)
- After adding .gitignore file and inclulde the name of the file that we want git to ignore, 
- `git rm -r --cached <file name>` to update the remote repo by deleting the files. Then we git add ., git commit and git push

### Git Stash
- we have made a change and without commiting the change, git doesn't allow us to change branch
- We use `git stash` to save the changes to commit later. To reach the changes later `git stash pop`

### Going Back in History
- `git log` to see a list of change history
- `git checkout <commit hash>` to go to specific time in history
- `git checkout <branch name>` to go back to most up-to-date branch

### Undo Commit
- git reset deletes the commit hash while git revert creates a new commit to revert the old commit's hash
- `git reset --hard HEAD~1` undo the last 1 commit and cancel the change 
- `git reset --soft HEAD~1` undo the last 1 commit but the change remains
- `git reset --hard HEAD~1` and `git push --force` discard the last change in local and remote repo (not preferabble when you work in a team)
- `git revert <commit hash>` creates a new commit to revert the old commit's change 
