# learn-git

## Create new repository
```bash
echo "# learn-git" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/eric-el-tan/learn-git.git
git push -u origin master
```
                
…or push an existing repository from the command line
```bash
git remote add origin https://github.com/eric-el-tan/learn-git.git
git push -u origin master
```

## Clone from repository
```
git clone https://github.com/oracle/docker-images
git clone https://github.com/oracle/docker-images docker-images222
git clone -b branch-asl-sprint-11-develop https://pdgitlab.haitcl.org/cims/cims-frontend-app cims-frontend-app_11
```

## Switch to branch orgin/master
```bash
cd /my-frontend-app
git status
git checkout origin/master
```
[Checkout](https://www.atlassian.com/git/tutorials/using-branches/git-checkout)
```bash
git checkout branch1   (make branch1 active)
git merge master     (merge current branch into master branch)
git checkout -b dummybranch
git checkout -b oldbranch newbranch
git checkout -d dummybranch
```

## [branch](https://www.jquery-az.com/list-branches-git)
list all branches in local and remote repositories is:

list only the remote branches
```
$ git branch -a
```
see the branches and their commits
```
$ git branch -r
```
see the branches and their commits
```
$ git show-branch
```

## Force Pull
```bash
git fetch --all
git reset --hard origin/master
git pull
```

## Update repository
```
git add README.md
git commit -m "add configure ubuntu"
git push -u origin master
```

## Credential Store
```bash
git config credential.helper store

git pull
enter username
enter password
(no more prompt for username password)

git config --global credential.helper "cache --timeout 7200"  (7200 seconds = 2 hr) 
git help credentials
```

## [Merge conflict](https://www.atlassian.com/git/tutorials/using-branches/merge-conflicts)
Need to study