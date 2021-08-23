# Vim

Vim is a text editor that runs in the terminal, and is installed on pretty much any machine. It's lightweight and fast, but has a steep learning curve! 

To open a file in vim, run

```
vim <filename>
```

If you find yourself trapped in vim, type `:q!` and press enter to escape!

## Modes in vim

Vim has three different "modes" for editing the text in a file. These are:

1. **Normal mode**: the default mode. In this mode, each letter on the keyboard has a special function. 
    - Press `Esc` at any time to get back to this mode.
2. **Insert mode**: this mode resembles a more convential text editor, allowing you to use the keyboard normally to insert text into the file. 
    - Access this mode by pressing `i` in normal mode
    - Exit this mode by pressing `Esc`
3. **Visual mode**: a mode for selecting blocks of text by using the letters on the keyboard to move around. Useful for copying and deleting text.
    - Access this mode by pressing `v` in normal mode
    - Exit this mode by pressing `Esc`

In normal mode, you can also enter vim's inbuilt command prompt by pressing `:`. Some common commands are:
- `:q`: **q**uit vim
- `:w`: **w**rite (save) the file
- `:wq`: **w**rite and **q**uit
- `:q!`: **q**uit without saving
- `:e <filename>`: open a file for **e**diting
- `:w <filename>`: **w**rite to a specific filename

## Basic navigation

These keys are used to quickly move the cursor in **normal** mode, or to change the region of text selection in **visual** mode.

Single-space movement:
- `h`: move one space left
- `j`: move one space down
- `k`: move one space up
- `l`: move one space right

Word movement:
- `w`: jump to the start of the next **w**ord
- `b`: jump **b**ack one word
- `e`: jump to the **e**nd of a word

Movement within a line:
- `0`: jump to the start of the line
- `^`: jump to the first character (that isn't a space) on the line
- `$`: jump to the end of the line

Movement within a file:
- `gg`: jump to first line of file
- `G`: jump to last line of file
- `<n>gg` / `<n>G` / `:<n>`: jump to line n

To move multiple spaces/words at once, type any number before a movement command to repeat that movement; e.g. `30l` would move the cursor 30 spaces to the right.

## Inserting text

Text insertion is done in **insert mode**. From a given cursor position in **normal mode**, there are several ways to enter insert mode, with each placing you in a different starting position:

- `i`: insert text before the cursor
- `a`: insert text after the cursor

- `I`: insert text at start of line
- `A`: insert text at end of line

- `o`: create new line below the cursor and enter insert mode
- `O`: create new line above the cursor and enter insert mode

Don't forget to return to **normal mode** by pressing `Esc` when you're done!

## Deleting text

To delete a single character:
- `x`: delete character under the cursor
- `X`: delete character before the cursor

To delete larger blocks of text:
- `d` + any movement command: **d**elete from cursor to end of movement. E.g.:
    - `de` to delete to end of word
    - `dG` to delete to end of file
    - `d20l` to delete 20 characters to the right
- `dd`: **d**elete whole line
- `D`: **d**elete from cursor to end of line (equivalent to `d$`)

## Copying and pasting

Vim has its own internal clipboard. Whenever you delete some text, the deleted text will automatically be saved to this clipboard (like the "cut" function in microsoft word).

To copy text to the clipboard without deleting it:
- `y` + any movement: copy ("**y**ank") from cursor to end of movement
- `yy`: **y**ank entire line

To paste the most recently copied text:
- `p`: **p**aste after cursor
- `P`: **p**aste before cursor

(You can also access your computer's clipboard as you normally would with `Ctrl-v` in **insert mode**)

## Visual mode

**Visual mode** makes deleting and copying easier and more intuitive! Enter it by pressing `v` from **normal mode**. Any movements performed in this mode will drag a selection box from the original cursor position to the position you have moved to. Press `y` to copy the selected text, or `d` to delete it.

There are also two special versions of this mode, entered by pressing:
- `V`: select entire lines of text at once
- `Ctrl-v`: select rectangular boxes of text

## Searching and replacing

To search for a particular string in the document:

- `/<string>`: search downwards through the file
- `?<string>`: search upwards through the file

Press `Enter` to perform the search. The cursor will automatically jump to the closest match. You can then jump through any subsequent matches:
- `n`: jump to next match in the direction of the search
- `N`: jump to previous match in the direction of the search

You can simultaneously search and replace strings using the `:s` command. 

Find and replace the **first** match on a **single** line:
```
:s/string1/string2/
```

Find and replace **all** matches on a **single** line (*g*lobal replacement):
```
:s/string1/string2/g
```

Find and replace **all** matches on **all** lines:
```
:%s/string1/string2/g
```

Vim's search and replace is extremely powerful if combined with Regular Expressions (RegEx) to use wildcards etc to create complex search terms. There are many RegEx guides and tutorials available online.

## Useful editing commands

- `u`: undo previous command
- `Ctrl-r`: redo previously undone command
- `.`: repeat previous command
- `>>`: indent the current line (or current visual selection)
- `<<`: unindent the current line (or current visual selection)

## Editing multiple files

When opening vim from the command line, give any number of file names to open multiple files:

```
vim <file1> <file2> <file3>
```

However, only be able to the first file in the list will be displayed in vim at first. 

You can also open additional files from inside vim using 

```
:e <filename>
```

which will bring the new file to the foreground. Any previously open files will still be open in vim even though they're not visible - these are called "buffers".

Navigating through buffers:
- `b <filename>`: bring a specific buffer to the foreground. Pressing `Tab` to autocomplete after `:b ` is a useful way to see the list of open buffers (note: you need to have `set wildmenu` turned on for this - see the "Customising vim" section)
- `:bprev`: bring previous buffer to the foreground.
- `:bn`: bring next buffer to the foreground.
- `:bd`: "delete" the current buffer (i.e. close the current file)

To view multiple buffers at once, the screen can be split into multiple windows:
- `:vsp`: create a vertical split
- `:sp`: create a horizontal split
- `:vsp <filename>`: open a new file and display it in a new vertical split

If you don't provide a filename, `:vsp` and `:sp` will simply display a copy of the file you're currently viewing. However, you can navigate between your open buffers within one of the windows using `:b` to show different buffers in different windows. 

Navigating between windows:
- `Ctrl-w w`: jump to next window
- `Ctrl-w` + `h`/`j`/`k`/`l`: jump to a window to the left/bottom/top/right 

A window can be closed by typing `:q` within the window; this removes the window, but doesn't close the file that was being displayed in it. That file will still be open in vim as a buffer. 

To save and quit all buffers, type `:xa`.

When opening vim from the command line, you can automatically display two files in a vertical split using

```
vim <file1> <file2> -O
```

(or use `-o` for an automatical horizontal split)

## Customising vim

Similar to the `.bashrc` file for configuring the bash environment, vim executes any commands in a file in the home directory called `.vimrc` whenever it is run. (An example vimrc file is [here](https://github.com/hpullen/dotfiles/blob/master/.vimrc)).

Some essential (or at least very useful) options to put in this file are:
- `syntax enable`: turn on syntax highlighting
- `set number`: display line numbers in left margin
- `set undofile`: save undo history for each file even after vim is closed, so it's still there when the file is reopened
- `set hlsearch`: highlight matches after performing a search
- `set incsearch`: highlight matches as you are typing in a search term
- `set wildmenu`: allow tab completion when entering commands with `:`

Some other nice but non-essential options:
- `set mouse=nicr`: allows you to move your cursor by clicking with the mouse; can be useful for beginners
- `set cursorline`: highlight the line the cursor is on so it's easier to see
- `set autoindent` and `set smartindent`: automatic indentation when starting a new line
- `set colorcolumn=80`: highlight the 80th column so it's easy to identify lines that are too long
- `colorscheme <scheme>`: set a colourscheme of choice (some options [here](https://vimcolors.com/); I use solarized dark)

The following code snippet makes the `Tab` key insert 4 space characters instead of a `Tab` character (this is important for python):
```
filetype off
filetype plugin indent on
set tabstop=4
set softtabstop=4
set shiftwidth=4
set expandtab
```

### Vim plugins

Many vim enthusiasts have written plugins to add extra functionality to vim (browse some of them [here](https://vimawesome.com/))! These can easily be added to the vim configuration using a plugin manager, such as [vim-plug](https://github.com/junegunn/vim-plug) (follow link for installation instructions).

Some nice plugins are:
* Automatic commenting based on filetype: [NERDcommenter](https://github.com/preservim/nerdcommenter) or [commentary](https://github.com/tpope/vim-commentary)
* Display file structure within vim: [NERDtree](https://github.com/preservim/nerdtree)
* Display and jump back through undo history: [undotree](https://github.com/mbbill/undotree)
* Check python code for PEP8 compliance: [flake8](https://github.com/nvie/vim-flake8)
* Commands for quickly adding/changing brackets/parentheses/quotes: [vim-surround](https://github.com/tpope/vim-surround)
* Code autocompletion: [YouCompleteMe](https://github.com/ycm-core/YouCompleteMe) (can be a bit tricky to set up, and unfortunately doesn't seem to work on the HEP cluster)


## More navigation

The word-jumping commands `w`, `b`, and `e` will stop at punctuation. Their capital-letter versions `W`, `B` and `E` can be used to jump between any pieces of text separated by whitespace; these are useful for navigating through code more quickly! E.g. to jump past some text `class.function("a")` would take several presses of the `w` key, but only one press of `W`.

Commands for jumping to a specific character:
- `f<char>`: jump to the next instance of a character ("**f**ind" a character)
- `F<char>`: jump to the previous instance of a character
- `t<char> `: jump to one space before the next instance of a character
- `T<char> `: jump to one space after the previous instance of a character
- `;`: repeat the previous `t`/`f`/`T`/`F` command in the same direction
- `,`: repeat the previous `t`/`f`/`T`/`F` command in the opposite direction

More useful jumping:
- `}`: jump to start of next paragraph
- `{`: jump to start of previous paragraph
- `])`: jump to next closing paranthesis (useful for jumping to end of an argument list in code)
- `[(`: jump to next opening paranthesis (useful for jumping to start of an argument list in code)

Scrolling:
- `Ctrl-u`: scroll page up
- `Ctrl-d`: scroll page down
- `zz`: scroll the line the cursor is on to centre of screen
- `zt`: scroll the line the cursor is on to top of screen
- `zb`: scroll the line the cursor is on to bottom of screen

## More text insertion

- `s`: delete character under the cursor and enter insert mode (equivalent to `x` + `i`)
- `c` + any movement: delete from cursor until end of movement and enter insert mode (equivalent to `d` + movement + `i`)
- `cc`: delete entire line and enter insert mode (equivalent to `dd` + `i`)
- `C`: delete from cursor to end of line and enter insert mode (equivalent to `D` + `i`)

You can also press `s` or `c` while in **visual mode** to delete any selected text and enter insert mode.

## More commands

### Advanced copy/paste

When text is deleted or copied, it's stored as the most recent entry in vim's internal "register" (clipboard). Pressing the paste key, `p`, only pastes the most recent entry. However, the older entries are still in there!

To view the register, type

```
:reg
```

This will show a list of register entries (each labelled by a `"` character followed by a letter/number/symbol) and the text contained within that entry. To paste the text from a specific entry, type the label followed by the `p` key. E.g. to paste the text stored under entry `"0`, type `"0p`.

By default, vim uses numbers and punctuation for its register labels. All of the letters of the alphabet are then available for storing text in custom registers. To copy text to somewhere safe where it won't be overwritten:

1. Pick a letter, e.g. `a`
2. Type the register label, `"a`
3. Perform the copy command, e.g. `yy` to copy the whole line

The copied text is now stored in register `a`, and can be pasted later with the command `"ap`.


### Macros

If there is a sequence of commands that you want to apply multiple times/in multiple places in the file, you can record that set of commands as a **macro** with the following method:

1. Pick a letter, e.g. `a` (note: this uses the same storage system as copied text, so be careful not to overwrite anything important!)
2. Press `qa` to start recording a macro
3. Perform any commands you want to record
4. Press `q` to stop recording

The register `a` will now contain the sequence of keystrokes that was pressed while recording. You can now repeat these keystrokes anywhere in the file by pressing `@a`.


### RegEx

ReGex is a powerful way of creating complex, flexible search terms.
Some useful ReGex special characters are:

- `.`: any character
- `\\w`: any "word" character (letter, number or underscore)
- `\\d`: any number
- `\\w`: any whitespace character
- `^`: start of a line
- `$`: end of a line
- `[some_chars]`: any of the characters in some_chars
- `[^some_chars]`: any character not in some_chars

The following modifiers can be added after a character:
- `*`: zero or more repeats of that character (e.g. the combination `.*` would search for any number of any character)
- `\+`: one or more repeats of that character
- `\{n\}`: n repeats of that character

When searching and replacing with `:s`, it is sometimes useful to use the search term inside the replacement term. This can be done with the `&` special character. For example, to put quotation marks around every word on a line:

```
:s/\w\+/"&"/g
```

* `:s` tells vim to search and replace on a single line
* `\\w\+` tells vim to search for combinations of 1 or more numbers, letters or underscores (i.e. to find a word)
* `"&"` tells vim to replace any matches with the matched string surrounded by quotation marks
* `g` tells vim to apply the replacement to all matches on the line (by default, only the first match would be replaced)

You can also define groups of characters in the search term to reference in the replacement term using parentheses: `\(` and `\)`. Each of these "groups" is referred to as `\\1`, `\\2`, etc in the replacement term, in the order in which the groups were defined. For example, to replace each word on a line with its first letter:

```
:s/\(\w\)\w*/\1/g
```

* `\(\\w\)`: defines a "group" containing the first letter of a word
* `\\w*`: the rest of the search term (any number of additional letters in the word)
* `\\1`: refers to the first group defined in the search term (i.e. the first letter of the word)
