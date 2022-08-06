# this is for how to use git

# start a new local repo on a folder

  git init

# create a new file and add it

  git add [filename]

# commint the added file to git

  git commit -m "[description]"

# show the commits history

  git log

# create a new branch from the current one

  git checkout -b [branchname] # create and goto
  git branch [branchname]

# delete a brach

  git branch -d [branchname]
  git branch -D [branchname] # force

# list branches

  git branch -A

# see what repo is this from

  git remote show

# push an existing local repo to a git remote repo

  git remote add origin [repoURL]
  git push -u origin master # -u is for push it to up-stream

# grab changes from the remote repo

  git pull --rebase origin

# go to a pull request made by some contributor an checkitout

  git checkout -b [pullrequestname] master
  git pull [repoURL] [pullrequestname]

# merge a pull request

  git merge --no-ff [pullrequestname] # --no-ff

# push changes made by pull request to master

  git push origin master

# Switch a repo from depricated password to SSH Key

git remote set-url origin [SSH_URL]

# Public key issue (Permission denied)

>https://stackoverflow.com/questions/12940626/github-error-message-permission-denied-publickey
