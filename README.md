In Git, the three areas (Working Directory, Staging Area, and Repository) are referred to as "areas" or "zones." 
Each area represents a specific stage in the typical Git workflow, allowing you to manage changes to your project effectively.

-  Working Directory: This area represents the directory on your local machine where you are actively working on your project. It contains the actual files that you are editing, creating, or deleting as you develop your code.

-  Staging Area (Index): The staging area is an intermediate area that comes between the Working Directory and the Repository. It acts as a holding area for changes that you want to include in the next commit. When you make modifications to files in the Working Directory, you use the git add command to move those changes to the Staging Area.

- Repository: The Repository is the Git database that stores the entire history and versioned data of your project. It is the central location where all the committed snapshots, branches, tags, and other Git objects reside. When you are ready to permanently save the changes you've staged in the Staging Area, you use the git commit command to create a new commit in the Repository.
When you create a new Git repository in a directory, it contains both the working directory and the staging area. As you make changes to files, you use 'git add' to move changes from the working directory to the staging area. Then, when you use 'git commit', the changes in the staging area are permanently recorded in the repository as a new commit.
There are two types of repository (your local machiene and remote machines) just like Docker in this case.
```bash
git config
git config --global user.name "[rfatolahzade]"

git config --global user.email "[r.rinland88@gmail.com]"
git config --global core.editor atom
git config --global --edit
```
#Used to list all the files that have to be committed:
```bash
git status
git status --long

git init
git status
git add
git commit -m ""
```
#Remove staged file:
```bash
git rm --cached  dummy.txt
```
#Remove All Staged Files/Directories (staged means all stuff those who added )
```bash
git rm --cached -r .
```

#Git diff Show changes between working directory & staging area and staging area & remote repository:
```bash
git diff [file] #Show changes between working directory and staging area
git diff --staged [file] #Shows any changes between the staging area and the repository.

```
#list of commits
```bash
git log
git log --oneline
git log -3 --oneline    ##3Last commits
git log -p
git log --stat
```
#Undo Changes:
#Before Add
```bash
git restore -- dummy
#After Add
git restore --staged dummy
```
#Undo commit:
First check out list of the commits:
```bash
git log --oneline
```
In my case:
```bash
5314de1 (HEAD -> master) M files
9d0eefb M files
caddc3f M files
29e89e3 init
```
I'm going to switch to caddc3f
```bash
git reset caddc3f
git reset --hard caddc3f
git checkout <commit hash>
git revert <commit hash>
```
- If you want to test the previous commit just do git checkout <test commit hash>; then you can test that last working version of your project.
- If you want to revert the last commit just do git revert <unwanted commit hash>; then you can push this new commit, which undid your previous commit.
- To fix the detached head do git checkout <current branch>.

# git branch:
```bash
git branch dev
git branch -a
git checkout dev
git checkout master
git branch -d develop #delete a branch
git push -d origin develop #delete a remote branch 
```
#Other way to create:
```bash
git checkout -b develop
```

#Merge:
```bash
git checkout master
git merge develop
git log --graph
```
#Git stash
#Save temp commits on a branch Without see Modified files on the other branch
#on your develop branch (in my case)
```bash
git stash
git stash save "Pre commit"
git stash list
git stash  show -p stash@{0}
git stash apply stash@{0}
git stash pop stash@{0}
git stash drop  stash@{1}
```
#Update branch from master (in my case)
```bash
git checkout develop
git rebase origin/master
git push
```
#.ignore file sample:
```bash
node_modules/
*.txt
!a.txt
```
#If you have had a commited file and now you wanna add it to ignore file:
```bash
git rm --cached -r .
git add .
git commit -m "M"
```


#Remote
```bash
git remote add origin https://github.com/rfinland/git-cheat-sheet.git
git remote
git branch -M master
git push -u origin master
git push -u origin develop
```

#bisect
```bash
git bisect start
git bisect good <Choose Hash when it was good>
#test it and add re-action (bad-good)
git bisect bad
#OR
git bisect good
```
```bash
When you found out which commit ruined everything then:
git bisect reset
```

#Create a ssh-key
Create a ssh key and then set in in github:

```bash
ssh-keygen -t ed25519 -C "#YOUREMAIL"
```
Set your pub key:
https://github.com/settings/keys

#Clone via ssh
After adding the pub key to your github,now you can clone your private repo via ssh
Make sure your ssh agent is running as well:
```bash
 eval "$(ssh-agent -s)"
```
List The agent identities:
```bash
ssh-add -L
```
if you aimed The agent has no identities, add your private key to list of identities via ssh-add command:
```bash
ssh-add ~/.ssh/id_ed25519
```

#git-clone-all
The best way that I test to clone all public repositories:

Installedpackages:
```bash
apt install python3-pip
pip3 install github-archive
```
To achieve all repose run:
```bash
github-archive --users rfatolahzade --clone
```
You should read help of github-archive if you want to clone special repos
To clone private repos un int manually (update needs)
```bash
git clone git@github.com:rfatolahzade/akube-pdf.git
git clone git@github.com:rfatolahzade/auseful-Doc.git
git clone git@github.com:rfatolahzade/omy-adventure.git
git clone git@github.com:rfatolahzade/anAWS-Training.git
git clone git@github.com:rfatolahzade/anAnsible-Kubespray.git
```

Your cloned repos are already in :
```bash
~/github-archive/repos/rfatolahzade
```


Below are some useful Git commands and best practices grouped based on where they will have an effect:
staging, local directory, and remote repository. 
Staging Area:
Add changes to the staging area:

```bash

git add <file(s)>       # Add specific files to the staging area
git add .              # Add all changes in the current directory to the staging area
git add -p             # Interactively review and add changes to the staging area
```
Remove changes from the staging area:

```bash

git restore --staged <file(s)>  # Remove specific file(s) from the staging area
git restore --staged .         # Remove all changes from the staging area
```
Review changes in the staging area:

```bash
git diff --staged        # Show the difference between the last commit and the staging area
```
Local Directory:
Commit changes:

```bash

git commit -m "Commit message"        # Commit staged changes with a commit message
git commit -a -m "Commit message"     # Commit all tracked changes (staged and unstaged)
git commit --amend                   # Amend the last commit with staged changes
```
Review commit history:

```bash

git log                # Show commit history
git log --oneline      # Show commit history in a compact format
```
Undo changes:

```bash

git restore <file(s)>  # Discard changes in working directory (unstaged)
git checkout <file(s)> # Undo changes and restore files to the last commit (unstaged)
```
Create and switch branches:

```bash

git branch <branch_name>     # Create a new branch
git checkout <branch_name>   # Switch to an existing branch
git checkout -b <branch_name> # Create and switch to a new branch
```
Merge branches:

```bash

git merge <branch_name>   # Merge specified branch into the current branch
```
Remote Repository:
Clone a repository:

```bash

git clone <repository_url>       # Clone a remote repository to your local machine
```
Push changes to a remote repository:

```bash

git push <remote_name> <branch_name>   # Push local commits to the remote branch
```
Fetch and pull changes from a remote repository:

```bash

git fetch <remote_name>           # Fetch changes from the remote repository
git pull <remote_name> <branch_name>  # Pull changes from the remote branch into the current branch
```
Review remote repositories and branches:

```bash
git remote              # List remote repositories
git remote -v           # Show remote repositories with URLs
git branch -r           # List remote branches
```
Create and manage remote branches:

```bash

git push -u <remote_name> <local_branch_name>  # Push a local branch and set up to track it remotely
git push <remote_name> --delete <branch_name>  # Delete a remote branch
```
