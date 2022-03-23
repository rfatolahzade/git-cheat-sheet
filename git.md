git config
git config --global user.name "[rfinland]"

git config --global user.email "[r.rinland88@gmail.com]"


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
git checkout -- dummy
