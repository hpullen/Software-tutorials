# Git

Git is a version control program that enables the user to create checkpoints in a project. The code can easily be reverted back to these checkpoints, and different version can be compared. Using git online (e.g. via GitHub, GitLab) provides a mechanism for sharing code with others.


## Using git locally

First, create a **repository** in which to store the project code. In the root directory of the project, this is done with the command

```
git init
```

### Staging and committing

To save any changes, you need to 
(a) "stage" the changes (create a list of files to be recorded)
(b) "commit" the list of staged changes (create a checkpoint containing those changes)

* Add any file to the "staging" list with the command

    ```
    git add <filename>
    ```

    or simply add all files in the current directory via

    ```
    git add .
    ```

    (this automatically adds the contents of any subdirectories too.)

* The staged changes can then be **committed** with the command

    ``` 
    git commit -m "Useful message describing your changes"
    ```

    The steps can be combined (i.e. stage all changes and commit them) with the command

    ```
    git commit -a -m "Useful message describing your changes"
    ```

* View a list of staged files and untracked changes at any time with
    ```
    git status -s
    ```

### Deleting, amending and resetting

* If you decide to remove a file from the repository, use the command

    ```
    git rm <filename>
    ```

    before performing a commit.

* If you realise you forgot to add something to a commit and don't want to make a whole new commit, you can stage the change then **amend** the previous checkpoint with the command

    ```
    git commit --amend
    ```

    This will open a text file in your editor; simply save and exit the file, and the commit will be amended.

* If you have **staged** some files (but not yet committed) and want to remove them from the staging list, use the command

    ```
    git reset
    ```

    Note this won't do anything to the files themselves; it just removes them from the staging list.

* If you have made changes since the last commit and want to completely discard them, run the command

    ```
    git reset --hard HEAD
    ```

    Be careful, this will erase all changes since the commit and **can't be undone!**


### Accessing previous versions

* One powerful feature of git is the ability to easily revert a project to a previous state. View a list of all previous commits with the command

    ``` 
    git log
    ```

    This will display the time, date, and message for each commit, as well as a unique ID number for each. 

* To revert to a commit with a certain ID, use the command

    ```
    git checkout <commit_ID>
    ```

    To get back to the newest commit, run

    ```
    git checkout HEAD
    ```

    (HEAD is a shortcut referring to the ID number of the newest commit).

    There is also a shortcut for going back N generations:

    ```
    git checkout HEAD~N
    ```

* Git won't let you checkout an old commit if you have untracked (i.e. uncommitted) changes in the latest version of the project. If you're not ready to commit these changes yet but still want to checkout an old version, you can **stash** the untracked changes:

    ```
    git stash
    ```

    To get the stashed changes back later, run

    ```
    git stash apply
    ```

    If decide you don't actually want the stashed changes, discard them with

    ```
    git stash drop
    ```

* Compare the current version of a file to a version in an older commit, without having to checkout the older commit:

    ```
    git diff <commit_ID> <filename>
    ```

### Tagging

To make certain commits easier to access, it may be useful to "tag" them (e.g. tagging specific versions of some code). Once a commit has been performed, it can be tagged using

```
git tag -a <tag> -m "Description of this version"
```
where `<tag>` is the tag of your choice, for example `v1.0`.

If you don't want to write a description, a tag can also be quickly created with 
```
git tag <tagname>
```

* A list of existing tags can be viewed with the command `git tag`.
* A tag can be deleted with the command `git tag -d <tagname>`.

Reverting back to a previous version using tags is very easy:
```
git checkout <tagname>
```
This removes the need to search through the git logs for the ID of a particular commit; you can instead access it via its tag.

### Branches

By default, commits are saved to a branch called "master". Sometimes, you may want to try something new without altering the master branch, and later merge this code with the master branch once everything is working. This is achieved by checking out a new branch:

```
git checkout -b my_branch
```

Now, any commits will be saved to `my_branch` instead of `master`.

* To list all branches and see which branch you are currently on:

    ```
    git branch list
    ```

* You can easily switch back to the master branch:

    ```
    git checkout master
    ```
    Any commits will be saved to the branch that was most recently checked out.

* To return to the new branch from the master branch, just use the `checkout` command again:

    ```
    git checkout my_branch
    ```

* To merge a branch with the master branch, first checkout the master branch, then run the `merge` command:

    ```
    git checkout master
    git merge my_branch
    ```

* If the master branch has also been edited since the new branch was created, this could lead to a **merge conflict**. The command `git show -s` will indicate which files contain conflicts. Text inside these files will show the conflicting parts from both commits. More details [here](https://docs.github.com/en/free-pro-team@latest/github/collaborating-with-issues-and-pull-requests/resolving-a-merge-conflict-using-the-command-line); the general procedure for fixing the conflict is:
    1. Identify which files have merge conflicts using `git show -s`
    2. Open each of these files in an editor, and find the lines where git has inserted text from both conflicting commits
    3. Delete the parts you don't want
    4. Save and close the files
    5. Stage the fixed files with `git add <filename>`
    6. Perform a commit, e.g. `git commit -m "fixed merge conflicts"`

* When you no longer need a branch, delete it using

    ``` 
    git branch -d my_branch
    ```

### The gitignore file

Sometimes you might not want git to add every single file when you run `git add .`; for example, you might might want to ignore large files or certain hidden files. To give git a list of filenames to ignore, create a file called `.gitignore` at the root directory of the repository. An example `.gitignore` might look like this:

```
# Ignore hidden files (beginning with .)
.*

# Don't ignore the .gitignore file
!.gitignore

# Ignore PDFs and PNGs, as these can be large
*.pdf
*.png
```

## Using git online

Using git remotely via a hosting service such as GitHub or GitLab is useful for backing up your own code, as well as for sharing/collaborating on code with others.

### Downloading someone else's repository

To download ("clone") a repository, copy the repository's URL from GitLab/GitHub and run the command

```
git clone <URL>
```

on the computer to which you want to download the code.

If the repository isn't publicly available, you will need a way to authenticate yourself. This can be done with a [personal access token](https://docs.gitlab.com/ee/user/profile/personal_access_tokens.html). When you attempt to clone the repository, you will be prompted for your username (for the Cambridge GitLab service, this is your CRSID) and a password (the personal token).

### Creating your own remote repository

1. On whichever hosting service you are using (e.g. https://codeshare.phy.cam.ac.uk/), click "New project". Give your project a name and decide whether you want it to be public or private.

2. Follow the instructions for either creating a brand new repository or uploading an existing local respository.

### Pushing and pulling

* Whenever you have made changes to a repository on your local machine and want to upload the changes to the remote repository, first perform a commit and then run:

```
git push origin master
```

Here, "origin" is the default name for the remote branch. You can also push any other branch to the remote repository via

```
git push origin my_branch
```

which allows you to keep track of multiple branches on GitLab.

* When changes have been made to the remote repository (e.g. one of your collaborators uploaded some changes), you can download the changes to your local machine with

```
git pull
```

### Submodules

* To add another git respository as a submodule of an existing repository, run:

```
git submodule add <url-of-submodule>
```

where the url is the same as the one you would use to clone the repo. This will create a directory with the name of the repo you have cloned.

* The version of submodule associated with your repo will be fixed as the latest one that existed when you added the submodule. To update your repo to use the latest version of the submodule, from inside your repo run:

```
git submodule update --remote
```

You should then commit and push this change to the remote of your own repo so that it knows to use the latest version.

* If someone else has updated the version of the submodule inside the remote repo, you can pull this to your own local version using:

```
git pull --recurse-submodules
```

or to make this happen automatically each time you use `git pull` in this repo, run:

```
git config submodule.recurse true
```

which will add this option to your git settings. (You can run this with the `--global` option to apply this setting to any repo on your machine.)

* When you clone a repo with submodules for the first time, in order to initialise the submodules you need to run:

```
git clone --recurse-submodules <url-of-repo>
```

If you forgot to add `--recurse-submodules` while cloning and want to restrospectively initialise the submodules, run:
```
git submodule update --init --recursive
```

