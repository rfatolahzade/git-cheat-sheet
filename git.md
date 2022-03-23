git config
git config --global user.name "[rfinland]"

git config --global user.email "[r.rinland88@gmail.com]"
git config --global core.editor atom
git config --global --edit
#Used to list all the files that have to be committeds
git status
git status --long

git init
git status
git add
git commit -m ""

#Remove staged file:
git rm --cached  dummy.txt

#Remove All Staged Files/Directories (staged means all stuff those who added )
git rm --cached -r .


#Git diff between what you added and what is
git diff

#list of commits
git log
git log --oneline
git log -3 --oneline
git log -p
git log --stat


#Undo Changes:
#Before Add
git restore -- dummy
#After Add
git restore --staged dummy

#Undo commit:
First
List of the commits:
git log --oneline

5314de1 (HEAD -> master) M files
9d0eefb M files
caddc3f M files
29e89e3 init
I'm going to switch to caddc3f
git reset caddc3f
git reset --hard caddc3f


# git branch:
git branch dev
git branch -a
git checkout dev
git checkout master
git branch -d dev
#Other way to create:
git checkout -b develop


#Merge:
git checkout master
git merge develop
git log --graph

#Git stash
#Save temp commits on a branch Without see Modified files on the other branch
#on your develop branch (in my case)
git stash
git stash save "Pre commit"
git stash list
git stash  show -p stash@{0}
git stash apply stash@{0}
git stash pop stash@{0}
git stash drop  stash@{1}



#.ignore file sample:
node_modules/
*.txt
!a.txt

#If you have had a commited file and now you wanna add it to ignore file:
git rm --cached -r .
git commit -a -m "M"