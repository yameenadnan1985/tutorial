**Github to Server**
**Good Video**
```

https://www.youtube.com/watch?v=H6UU7TsyrGs&t=322s

```

**How to setup**
```
# Go to your github repo and click actions and click on "set up a workflow yourself"

```

**Code for main.yml**
```
on: 
  push:
    branches: [main]
name: "Publish Website1"
jobs:
  web-deploy:
    name: 🚀 Deploy Website Every Commit
    runs-on: ubuntu-latest
    steps:
    - name: 🚚 Get Latest Code
      uses: actions/checkout@v3
    
    - name: 📂 Sync Files
      uses: SamKirkland/web-deploy@v1
      with:
        target-server: "138.197.161.147"
        remote-user: "root"
        private-ssh-key: ${{ secrets.SSH_PRIVATE_KEY }}
        destination-path: "/var/www/html/"
```
