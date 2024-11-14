# Git Cheat sheet by Michal Hucko
Basic config setup before first commit:
```bash
$ git config --global user.name "Michal Hucko"
$ git config --global user.email michal_hucko@hucko.com

# List current config
$ git config --list 

# Init git repo
$ git init 
```
Working with changes:
```bash
# Check staging area
$ git status

# Add changes to staging area  
$ git add file.py     # add file.py 
$ git add .           # add all file from current dir   
$ git add *.py        # add all python files from current dir

# Create commit
$ git commit -m "Create commit using imperative commit message"
$ git commit          # create commit with VIM prompt 

# Checking commit history
$ git log             
$ git log --oneline  
$ git log --oneline --graph

$ git rm file.py                # remove file from tracking and working tree
$ git mv file.py new_file.py    # rename file.py 
```

Working with branches:
```bash
$ git branch        # list all local branches 
$ git branch -r     # list all remote branches
$ git branch -1     # list all branches

$ git branch new_branch           # create new branch (no swithing to new branch)
$ git branch -d branch_name       # delete branch

$ git checkout <branch_name>      # switch HEAD to branch_name
$ git checkout -b <branch_name>   # create new branch and switch to it
```

Merging branches
``` bash
# To merge branch A to B make sure you are in the B branch 
$ git checkout B
$ git merge A
```

Working with remotes 
```bash
# First genrate SSH keypair 
$ ssh-keygen -o 

# Get the public key at paste it into github settings 
$ cat ~/.ssh/id_rsa.pub

# Get synced remotes 
$ git remote 
$ git remote -v 

# Add new remote 
$ git remote add <remote_name> <remote_address>

# push to remote 
$ git push <remote_name> <local_branch_name>
```

Joining new project
```bash
# First make sure to setup ssh key pair

# Clone the remote repository 
$ git clone <remote_repo_url>

# To track remote branch in your local branch 
$ git checkout -b <branch_name> <remote_name>/<remote_branch_name>
# e.g
$ git checkout -b test_branch origin/test_branch

# Update locally tracked branch 
$ git pull 

# Or 
$ git fetch <branch_name>
$ git merge <remote_name>/<branch_name>
```

Going back in time 
```bash
# Only use git reset when working with local branch (i.e. you haven't pushed your changes yet), you dont want to reset someone else changes
# Undo git add (remove staged changes)
$ git reset 
$ git reset <file_name>

# Undo and remove all uncommitted changes 
$ git reset --hard 
$ git reset --hard <file_name>

# Move branch to certain commit in history 
$ git log --oneline             # list commits
$ git reset --soft <commit_id>  # keep diffs in staging area
$ git reset --mixed <commit_id> # dont keep diffs in staging area
$ git reset --hard <commit_id>  # REMOVE CHANGES FOR EVER !!!!!! VERY DANGEROUS

# Move head to certain commit
$ git checkout <commit_id>      # CAREFUL its read only state
$ git switch -                  # move HEAD back to previous position
$ git switch -c <new-branch>    # create new branch from current commit
```


Using Tags 
```bash
# List tags
$ git tag

# create a new lightweight tag (mostly used for local tagging, not really pushed to remote)
$ git tag <tag-name>

# e.g
$ git tag v1.0.0

# create an annotated tag (stores some metadata, like a message, used when pushing tags to remote)
$ git tag -a <tag-name> -m <message>

#e.g
$ git tag -a v1.0.0 -m "My first release"

# create a tag from a specific commit
$ git tag -a <tag-name> -m <message> <commit-hash>

# e.g
$ git tag -a v0.9.9 -m "Prerelease version" 67830a4

$ git tag 

# remove a tag
$ git tag -d <tag-name>

#e.g
$ git tag -d v1.0.0

# push tags to remote

$ git push --tags

# Switch head to a specific tag
$ git checkout <tag-name>

#e.g
$ git checkout v1.0.0 # You will be in a read only state

# Switch head to a specific tag in a new branch
$ git switch -c <new-branch>

#e.g
$ git switch -c testing_v1.0.0
```