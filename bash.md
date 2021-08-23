# Bash

Bash is the default command line language on most systems. Some useful shortcuts when typing bash commands are

* `tab`: autocomplete the name of a command or file
* &#8593;: scroll through previous commands
* `ctrl-r`: search command history
* `ctrl-a`: jump to start of line
* `ctrl-e`: jump to end of line
* `ctrl-w`: erase a word
* `ctrl-u`: erase whole line
* `alt-b` / `alt-f`: jump backwards/forwards by one word

Once a command is running, the following shortcuts can be useful:
* `Ctrl-c`: cancel the command
* `Ctrl-z`: suspend the command (use the command `fg` to continue the command)

## Navigating

By default, when you start a bash session you will be in your "home" directory. The following commands are useful for navigating through the file system:

* `pwd`: **p**rint **w**orking **d**irectory (print the path to your current location)
* `ls`: **l**i**s**t files in current directory
    - `ls -a`: also show hidden files (files with names beginning with `.`)
    - `ls -l`: print extra details for each file, such as dates/sizes
* `cd <directory>`: **c**hange **d**irectory
    - `cd ..`: go up one directory
    - `cd ~` (or just `cd`): go to home directory
    - `cd -`: go to previous directory
* `clear`: clear the screen

The wildcard character, `*`, is also useful when dealing with files; e.g. `ls *` will list the files inside every subdirectory in the current directory.

## Basic file commands

Many tasks in bash involve dealing with files. To edit the contents of a file, use favourite editor, e.g.

`vim <filename>` (see [vim](vim.md) guide here)

The following bash commands are useful when dealing with files and directories:

* `mkdir <dirname>`: **m**a**k**e a new **dir**ectory
* `mv <filename> <directory/new_file>`: **m**o**v**e a file to either an existing directory or a new name (used for renaming files as well as moving them)
* `cp <filename> <directory/new_file>`: **c**o**p**y a file to either an existing directory or a new name
    * `cp -r <directory> <new_location>`: **r**ecursively copy a directory and its contents
* `rm <filename>`: **r**e**m**ove a file (be careful; this can't be undone!)
    * `rm -r <dirname>` will recursively delete a directory and its contents (again, be careful!)
    * `rmdir <dirname>` will delete an empty directory
* `cat <filename>`: print the contents of a file
    * `head -n <filename>`: print the first n lines of a file
    * `tail -n <filename>`: print the last n lines of a file

## Accessing a remote machine

To log into another shell remotely, use the "**s**ecure **sh**ell" (`ssh`) command:

`ssh -Y <username>@<machine>.hep.phy.cam.ac.uk`

* `<username>` is your username on the HEP system
* `<machine>` is the name of the HEP computers, e.g. `pcnk`
* The `-Y` option enables forwarding graphics from the HEP machine to your local machine

To log out, use the `exit` command.

Files can be copied from a remote machine to your local machine with:

`scp <username>@<machine>.hep.phy.cam.ac.uk:/path/to/file .`

This command will copy the specified file to your current directory (referred to as `.`).

* `scp <username>@<machine>.hep.phy.cam.ac.uk:/path/to/file path/on/local/machine`: copy to a specific location on local machine.
* `scp -r <username>@<machine>.hep.phy.cam.ac.uk:/path/to/directory .`: **r**ecursively copy a directory and its contents to your current directory.

Files can be copied from your local machine to a remote machine with:

`scp <filename> <username>@<machine>.hep.phy.cam.ac.uk:/path/to/copy/to`

### ssh keys

You can avoid typing in your password every time you log into a remote server by creating an **ssh key**. 

Setting up an ssh key to a remote server:

1. On your local machine, create the key:
    ```
    ssh-keygen
    ```
    You will be prompted to choose a location in which to save the key; press `Enter` to save to the default location.

    Enter a **passcode** of your choice when prompted.

    This will create a **public key** in `~/.ssh/id_rsa.pub` and a **private key** in `~/.ssh/id_rsa`.

2. Copy the **public key** to the remote server:
    ```
    scp ~/.ssh/id_rsa.pub <username>@<machine>.hep.phy.cam.ac.uk:~/.ssh
    ```
    (note: you might need to make sure a directory called `~/.ssh` exists on the remote machine first)

Now when you `ssh` into the remote machine, you will be prompted for your new **passcode** instead of your full password.

The passcode can then be added to the keychain on MacOS, so you don't have to type it in at all. To do this:

1. Open the file `~/.ssh/config` (you might have to create this if it doesn't exist yet). Add the following text:

    ```
    Host *
    AddKeysToAgent yes
    UseKeychain yes
    IdentityFile ~/.ssh/id_rsa
    ```

2. Launch an ssh-agent:

    ```
    eval $(ssh-agent -s)
    ```

3. Add your key:

    ```
    ssh-add -K ~/.ssh/id_rsa
    ```

Now you should be able to log into the remote server without having to enter a passcode at all.

## Useful command line tools

By default, there are many useful command line tools installed on most machines. Some tools worth knowing about are:

* `man <command>`: display the manual for a command.

* `which <command>`: check whether a command exists, and see where the executable for that command is saved.

* `grep <text> <filename(s)>`: search for occurences of text within a file (or multiple files).
    * Use the `-r` option to search recursively within directories.
    * Use the `--color` option for coloured output (or set `alias grep="grep --color"` in your `.bashrc`; see the "Customising your shell" section).
    * Use the `-i` option for a case-insensitive search.
    * Use the `-l` option to just print the names of files with matches, and not the matching text.

    Example: search recursively for all files containing the word "word" within the current directory:
    `grep -r -l "word" .`

* `diff <file1> <file2>`: print out differences between two files.
    * A nice alternative to install is [colordiff](https://www.colordiff.org/), which produces a coloured output.
    * Another option is vimdiff, which interactively compares the files in the vim editor.

* `find`: search for files matching some criteria.
    * E.g. find all text files in current directory: `find . -name "*.txt"`.
    * The option `-maxdepth` can help limit your search in directories with many levels of subdirectory, e.g. `find . -maxdepth 2 -name "*.txt"`.
    * Lots of other options: file size, date, etc.

* `top`: list the processes running on the machine you are logged into and their memory usage - useful on the HEP cluster to check whether people are running intensive jobs on your machine.

* Some useful commands for processing text are `sed` and `awk` - plenty of tutorials online for these.

## Redirecting output

When you run a command, instead of printing the output to the terminal you can redirect it somewhere else. Some examples are:

* `<command> > <filename>`: write the output of the command to a file, overwriting any previous file contents.
* `<command> >> <filename>`: write the output of the command to a file, adding it to the end of any previous file contents.
* `<command> | tee <filename>`: print the output to the terminal and also write it to a file.

By default, these commands will only write the standard output (`stdout`) and not any errors (`stderr`) to the file. If you also want to redirect the error, use the following commands:

* `<command> &> <filename>`
* `<command> &>> <filename>`
* `<command> |& tee <filename>`

More generally, the pipe operator `|` can be used to pass the output from one command to the input of another command.

A command can also be run in the **background** by adding a `&` at the end, i.e. `<command> <arguments> &`. To bring the process to the foreground, run `fg`.

## Variables in bash 

* **Variables** can be stored in bash, and referenced by a `$` sign followed by the variable name.
* **Environment variables** are variables that are exported when you start a new bash session. Some important environment variables are:
    * `$HOME`: location of your home directory.
    * `$USER`: your username.
    * `$HOST`: name of the machine you are logged into.
    * `$PATH`: a list of filepaths telling bash where to look for executables. If you try to run an executable that isn't in the current directory or the `$PATH` list, it won't work!

* The easiest way to see the value of a variable is with the `echo` command, which prints text to the terminal, e.g. `echo $PATH`.

## Customising your shell

When you launch a new bash shell, any commands within a file called `.bashrc` (located in the home directory) are automatically run. You can edit this file to add any useful commands that you want to run in every new shell.

* One useful command is `alias`, which lets you define new commands from combinations of existing commands. For example, to create a shortcut that clears the screen and shows the contents of the current directory:

    `alias cls="clear && ls"`

* You can also use the `.bashrc` file to customise the **prompt** (the string of text on the left-hand side of the screen before every command) by editing and exporting the `PS1` string. An easy tool for making a custom prompt is [here](http://ezprompt.net/).

* There are several popular alternatives to bash, e.g. zsh, which has the core functionality of bash with many additional features - a guide to getting started with zsh is [here](https://medium.com/swlh/power-up-your-terminal-using-oh-my-zsh-iterm2-c5a03f73a9fb). 

## Bash scripts

If you want to run a set of commands multiple times, or run with different arguments each time, it may be useful to create a bash file (a text file ending with the extension `.sh`). This file can be run from the command line via

`sh my_file.sh`

Arguments can be passed to this script when the command is run; they are accessed within the file as `$1`, `$2`, etc, for the first and second arguments, respectively. The script can be run with arguments via

`sh my_file.sh <arg1> <arg2>`

Bash is a Turing-complete programming language, and has all the functionality you might expect, for example:

**For** loops:

```
for i in thing1 thing2 thing3; do
    <some_command> $i
done
```

This can be useful in conjunction with the wildcard operator, `*`, e.g.

```
for FILE in *; do
    <some_command> $FILE
done
```
to apply some command to every file in the current directory.

**If** statements:

```
if [[ $PARAMETER == 3 ]]; then
    do_something
fi
```
(note: the spaces inside the brackets are important!)

## Additional resources

- [LinkedIn Learning](https://help.uis.cam.ac.uk/service/support/training/linkedin-learning-info) (sign in using @cam account)
  - [Learning Linux command line](https://www.linkedin.com/learning/learning-linux-command-line-2/learning-linux-command-line)
  - [Linux: bash shell and scripts](https://www.linkedin.com/learning/linux-bash-shell-and-scripts)
  - [Learning bash scripting](https://www.linkedin.com/learning/learning-bash-scripting)
