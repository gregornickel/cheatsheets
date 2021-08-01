# Vim 

My personal summary of vimtutor with the most useful commands.

## Commands

### Open/write

- Open a file from the shell prompt `vim filename`
- Save changes made to the text `:w filename`

### Exiting

- `esq` to switch to command mode
- Exit the editor and discard any changes `:q!` 
- Save file and exit `:wq`

### Navigate

- Moving the cursor: `h` (left), `j` (down), `k` (up), `l` (right)
- Move the curser a word forward `w`
- Move the curser to the end of a word `e`
- Move to the start of a line `0`
- Move to the end of a line `$`
- Move to the bottom of the file `G`
- Move to the start of the file `gg`
- Move to a specific line by typing `number + G`
  - `ctrl + g` shows the location in the file

### Delete 

- Delete single character: move curser to character `x`
- Delete a word: move curser to word `dw`
- Delete from the current character to the end of the word `de`
- Delete the end of a line `d$`
- Delete a whole line `dd`
- Join current line and the next line (remove newline) `J`Insert

- Insert: presse`i` to insert text
- Append: press `A`, it does not matter at which position thr cursor is
- Put a previously deleted text after the curser `p`

### Replace/change

- Replace a character at the curser `r`
- Change until the end of a word `ce`
- Delete the whole line and switch to insert mode `cc`

### Undo and redo

- Undo the last command `u`
- Undo all changes to a line `U`
- Redo (undo the undo's) `ctrl + r`

### Search 

- Search with `/` followed by the phrase to search for
  - Jump to the next occursion of the phrase `n`
  - Jump to the previous occursion of the phrase `N`
- Search in backward direction `?`
- Find a matching parenthesis by placing the curser on any (, [, or { and type `%`

### Substitute 

- Substitute new for the first old in the current line `:s/old/new`
  - Substitute all 'old's on a line `:s/old/new/g`
  - Substitute phrases between two line #'s type `:#,#s/old/new/g`
  - Substitute all occurrences in the file type `:%s/old/new/g`
  - To ask for confirmation each time add c `:%s/old/new/gc`

### External command 

- Execute an external command with `:!` followed by the command



## Explanations 

### Operator/motion

- `operator [number]  motion`
  - `operator` is what to do, such as d for delete
  - `[number]` is an optional count to repeat the motion
  - `motion` moves over the text to operate on
    - `w` (word)
    - `$` (end of line)

## Configuration File

For a user specific configuration of Vim create a **.vimrc** file in the HOME directory of the user. You can create a .vimrc file with:

```shell
touch ~/.vimrc
```

Open the .vimrc file with:

```shell
vim ~/.vimrc
```

## Plugin Manager

I am using vim-plug a minimalist Vim plugin manager ([Github](https://github.com/junegunn/vim-plug)).

### Installation

```shell
curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```

### Add Plugin

1. Add the plugins to the `.vimrc` file.
```vim
" List of plugins managed by vim-plug (will be downloaded to specified dir)
call plug#begin(has('nvim') ? stdpath('data') . '/plugged' : '~/.vim/plugged')
  Plug 'vim-airline/vim-airline'
  Plug 'preservim/nerdtree'
  Plug 'sonph/onehalf', { 'rtp': 'vim' }
call plug#end()
```
2. Reload your Vim configuration file (`:source ~/.vimrc`) or restart Vim, and run `:PlugInstall` to install the plugins.

### Remove Plugin

Remove the line from the `.vimrc` file. Quit and restart Vim, and run `:PlugClean`. Confirm the prompt to delete the directory with type `Y` .

### Ctags

Ctags is a programming tool that generates an index (or tag) file of names found in source and header files. The vim plugin tagbar requires ctags. With ctags it is possible to jump to functions with `ctrl + ]`. 

#### Installation

Install with homebrew:

```shell
brew install ctags
```

MacOS has a ctags version installed. Afterwards, set the alias to the new version:

```shell
alias ctags="`brew --prefix`/bin/ctags"
alias ctags >> ~/.zshrc
```

The second line will add `ctags=/usr/local/bin/ctags` to the .zshrc file.

Add `set tags=tags` to the `.vimrc` file with:

```vim
set tags=tags
```
