# Git to Github to Server
```
# local PC push the changes to github
git push origin 1.4.0
```

**In remote install git**
```
apt update or sudo apt update
apt install git or sudo apt install git
git --version
```

**Start empty git repo**
```
git init
```

**After git init move .gitignore from local to remote.**

**Add contents in git**
```
git add .
git commit -m "First commit"
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

**Set Permissions**
```
# To see file permissions do this
git ls-files --stage
# To change file permissions do this. P.S: We can only set permissions to executable. 
# Read/Write permissions we will menually have to set
git update-index --chmod=+x index.php
git commit -m "Changing file permissions"
```
# Done

**Get list of conflicted files in Git?**
```
git diff --name-only --diff-filter=U --relative
```

**Get list of remote servers**
```
git remote -v
```

**Add server**
```
git remote add dev root@138.197.161.147:/var/www/html/.git
```
