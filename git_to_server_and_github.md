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
