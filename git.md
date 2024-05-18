# Git

Git version control systems, most used commands and some special commands I rarely need.

## Git setup

After installation Git should be configured with name and email address. Git uses this information for every commit.

```shell
git config --global --edit
```

With the `--global` option the configuration is only necessary once. Git will use the information for all projects.  If a different name or email address is required for a specific project, the command without the `--global` option can overwrite the information within that project.

Check settings: 

```shell
git config --list
```

## Repository setup

First, you need to create a new repository or download an existing remote repository.

### Create new repository

If there is no remote repository yet and you want to create a new local git repository, first change with `cd` to the folder you want to manage with git and create a new git repository with it:

```shell
git init
```

### Clone existing repository 

```shell
git clone remote_repo_path
```

### Update remote repository path
```shell
git remote set-url origin https://github.com/USERNAME/REPOSITORY.git
```

Check the remote repository url with: `git remote -v`

### Set local username and email 

If you would like to set a username or email different from the global setting you can do so with:
```shell
git config user.name "Your Name"
git config user.email email@address.com
```

You can check your settings with:
```shell
git config --local -l
```

## Typical workflow

A local git repository consists of three "instances". The first is your **working directory**, which contains the actual files. The second is the **index** (also called stage or cache) that caches information about the working directory and the changes to be committed. The last one is the **HEAD** pointing to your last commit.

With `git add` you can add changes to the index. For single files with:

```shell
git add -f filename
```

For all files with (except the cases in .gitignore):

```shell
git add *
```

Check your staged files with:

```shell
git status
```

To unstage a file you can use:

```shell
git reset filename
```

Or unstage everthing at once:

```shell
git reset HEAD --
```

Now the mentioned files are staged and ready for commit. Changes are confirmed with a commit:

```shell
git commit -m "Commit message"
```

For a commit message with multiple lines use `git commit` and add your commit message with vim afterwards.

Now the changes are in the HEAD, but not yet in the remote repository. You need to push the changes in your local repository up to the remote repository, with `git push`:

```shell
git push origin branch_name
```

The default remote repository is called "origin".

#### Commit history 

```shell
git log —oneline
```

Reset the current branch with a previous commit:

```shell
git reset —hard <commit number>
```

### Update your repository

To update your local repository with the latest changes:

```shell
git pull
```

To download the changes first use ```fetch``` and then merge them with your stand ```merge```.

If you want to create a new branch `feature2` that tracks the remote branch `feature`:

```shell
git checkout -b feature2 origin/feature
```

To merge new commits added to the remote branch `feature` to your local branch you are currently in use: 

```shell
git pull origin feature
```

### Branching

#### Workflow

Check the current branch

```shell
git branch
```

Switch between branches

```shell
git checkout master
```

#### New branch

Create a new branch "feature_x" with:

```shell
git checkout -b feature_x
```

Upload a new branch, the branch is not available to others until you upload it to your remote repository:

```shell
git push origin feature_x
```

#### Merge branch

First switch to the branch you want to merge to with `git checkout`and then merge with: 

```shell
git merge feature_x
```

Cancel merge:

```shell
git merge --abort
```

#### Delete branch

Delete local branch:

```shell
git branch -d feature_x
```

Delete remote branch:

```shell
git push origin --delete feature_x
```

## Useful and used occasionally

### Reset local files

Reset the local changes to a file, assuming the file was not committed, or added to the index:

```shell
git checkout -- filename
```

If the file is already added it to the index, but not committed:

```shell
git reset HEAD filename
git checkout -- filename
```

Assuming the file is committed you can reset from the master branch:

```shell
git checkout origin/master filename
```

Undo the latest local commit:

```shell
git reset HEAD~
```

### Reset local repository with remote repository

Get your local branch to exactly match the remote branch can be done in two steps: 

``` shell
git fetch origin 
git reset --hard origin/master 
```

### Rename/move files or folder
```shell
git mv old_fileorfoldername new_name
```
Case sensitive renaming, e.g. from casesensitive to CaseSensitive:

```shell
git mv casesensitive tmp
git mv tmp CaseSensitive
```

(Git can't move files into or out of a repository)

##### Delete a file

```shell
git rm filename
```

##### Delete a folder

```shell
git rm -r foldername
```

##### Remove a file from Git repository without deleting it from the local filesystem

For a single file:

```shell
git rm --cached filename
```

and for a single directory:

```shell
git rm --cached -r directoryname
```

### Git Submodules

You can add a git submodule to your project with:
```shell
git submodule add <remote_url> <destination_folder>
```

When adding a git submodule, the submodule will be staged and as a consequence you need to commit your submodule. 

#### Update a git submodule

```shell
git submodule update --remote --merge
```
In order to update an existing git submodule with the `--remote` command you don't need to run `git pull` commands for each submodule. 

## .gitignore

Specify the files and folder which should not be tracked. The `.gitignore` file needs to be placed in the repository folder. 

```sh
# macOS
.DS_Store

# Thumbnails
._*

# Files being edited
*~

# Make and build files
*.o
*/build
```

## Git hooks

To create a global hook we create a git template to hold our global hook and add the hook to our individual git repository afterwards. 

1. Create a git template, e.g. in our home directory:
```sh
git config --global init.templatedir '~/.git-templates'
```
2. Create a directory for the global hooks:
```sh
mkdir -p ~/.git-templates/hooks
```
3. Write our hook: `vim ~/git-templates/hooks/pre-commit`. Example hook:
```sh
#!/bin/sh

# Fetch nocheckins when trying to commit
# This only works for staged changes, there is no hook for the git add command
echo "" && git grep -i --cached --line-number "nocheckin" && echo "Error: 'nocheckin' found, commit failed" && exit 1
```
4. Make sure the hook is executable:
```sh
chmod a+x ~/.git-templates/hooks/pre-commit
```
5. Re-initialize each existing repository to add the hook: (Note: Changes are not added, if a local hook already exists.)
```sh
git init
```


## Reraly used

### Create a new repository from subfolder

New repository with full commit history.

```shell
git clone remote_repo_path
cd repo_folder
git filter-branch --prune-empty --subdirectory-filter subfolder -- --all
cd ..
mv repo_folder new_folder_name
cd new_folder_name
git remote show origin
git remote set-url origin new_remote_repo_path
git remote set-head origin master
git remote show origin
git push -u origin --all
git push -u origin --tags
```
