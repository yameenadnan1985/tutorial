Complete Merge + Rebase Process + Delete process
1- Checkout to master branch
2- git merge branch name i,e git merge COL196
3- git branch -D COL196   // Remove the branch name from local
4- git push origin master // Push the changes to master
5- git push origin :COL196 // Delete branch from github
6- git checkout Existing Branch i,e git rebase master
7- git stash
8- git stash apply
