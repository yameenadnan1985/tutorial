**Complete Merge + Rebase Process + Delete process**

1- Checkout to master branch

2- git merge branch name i,e git merge COL196

3- git branch -D COL196   // Remove the branch name from local

4- git push origin master // Push the changes to master

5- git push origin :COL196 // Delete branch from github

6- git checkout Existing Branch i,e git rebase master

7- git stash

8- git stash apply

**Remove a git commit which has not been pushed**
```
git reset HEAD~1
```
**See specific commit and revert it**
```
git checkout master
git log
# It will show a list of all commits
git show 1fb6b315a741520cdb1cb986ad25d2d8954481ef
git revert 1fb6b315a741520cdb1cb986ad25d2d8954481ef
```
**Get list of all modified files after specific date**
```
git log --since="2021-10-21" --name-only --pretty=format: | sort > changed-files.txt
```
**Take all the files modified on certain date**
```
If you use TortoiseGIt, it provides this too.
Choose the folder, in explorer
Right click,Choose menu, TortoiseGit-> Show Log.

Select working directory and the last commiitted version.
Right click. Compare revisions. Select files you want to save/export.
Right Click. Export to folder. Done.
```
**If have more than 1 github accounts**
```
https://stackoverflow.com/questions/21160774/github-error-key-already-in-use
```

**Git get list of remote Servers**
```
git remote -v
```

**Get list of conflicted files in Git?**
```
git diff --name-only --diff-filter=U --relative
```

**How to ignore a file in git**
```
# Add file/directory path in .gitignore
Example: .gitignore
assets/globalpayments/app_id.txt

# Remove the file from from cache of git so that next time it does not track file 
git rm --cached assets/globalpayments/app_id.txt
```
