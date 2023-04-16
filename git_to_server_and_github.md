# Git to Github to Server
```
# local PC push the changes to github
git push origin 1.4.0

# In remote install github and pull the changes
git init
git add .
# Move .gitignore file to server
git commit -m "First git pull"
git remote add origin git@github.com:Grindyzer/Colibriwww.git
git pull origin main --allow-unrelated-histories
# If receive this error
# error: The following untracked working tree files would be overwritten by merge:
# ...
# Please move or remove them before you merge.
# Aborting
# Then use these commands
git reset --hard origin/main
```
# Set permissions

```
# To see file permissions do this
git ls-files --stage
# To change file permissions do this. P.S: We can only set permissions to executable. 
# Read/Write permissions we will menually have to set
git update-index --chmod=+x index.php
git commit -m "Changing file permissions"
```
# fetch from the default remote, origin
git fetch
# create a branch at your current master
git branch old-master
# reset to origin's master
git reset --hard origin/master
# merge your old master, keeping "our" (origin/master's) content
git merge -s ours old-master

git merge --allow-unrelated-histories -s ours old-master

git pull origin main --allow-unrelated-histories
```
# Done

# Other details

**Get list of conflicted files in Git?**
```
git diff --name-only --diff-filter=U --relative
```


**Git to Server**
**Good Video**
```
https://www.youtube.com/watch?v=H6UU7TsyrGs&t=322s
```

**Setup git on server**
```
# Login to SSH Server and go to location where you want to deploy your files.
cd /var/www/html/
git init --bare .git
cd .git/hooks/
# Create new files inside hooks
touch post-receive
vi post-receive
# Inside file put this content



#!/bin/sh
# checkout files. Add path where to deploy files. and path to git repo 
git --work-tree=/var/www/html --git-dir=/var/www/html/.git checkout -f


# Save the file and never forget to give it executable permissions
chmod +x post-receive

# Now go to your local system and type
git remote add dev root@138.197.161.147:/var/www/html/.git
# branch in local git repo and branch in remote git repo must match.
git push --set-upstream dev master
# For next time
git push dev master
```

**Save "Specific Local Directory" into the "Root Directory" of remote server**
```
// git subtree push --prefix directory_name remote_server_name remote_branch 
Example:
git subtree push --prefix www dev master
```

**Subtree Slow**
```
git subtree split --rejoin --prefix Sub_Directory Last_Commit
Example:
git subtree split --rejoin --prefix data/www 385f4e878f930358ee1caf44f0adbe43f5ca2238
```


**Get list of remote servers**
```
git remote -v
```

**Add server**
```
git remote add dev root@138.197.161.147:/var/www/html/.git
```

**Remote server**
```
git remote remove dev
```
