## Hotkeys
### Movement
- `ctrl+a` : move your cursor to the beginning of the line
- `ctrl+e` : move your cursor to the end of the line
- `ctrl+k` : delete any characters from your cursor to the end of the line
- `ctrl+u` : delete any characters from your cursor to the beginning of the line
- `ctrl+w` : delete the previous word

### Process/Command
- `!!` : run previous command
- `ctrl+c` : kill active process
- `ctrl+s` : suspend active process
- `ctrl+z` : put active process in bg
- `fg %x` : process with id x in fg (defaults to actively suspended process if no arg)

## Useful Shortcuts and Commands
- `ls` – List directory contents
- `cd` – Change the current directory
- `pwd` – Print current working directory
- `echo` – Print text to the terminal
- `cat` – Concatenate and display file contents
- `touch` – Create an empty file or update timestamp
- `cp` – Copy files or directories
- `mv` – Move or rename files or directories
- `rm` – Remove files or directories
- `ln` – Create hard or symbolic links
- `less` – View file content one page at a time
- `more` – View file content scrollable (simpler than `less`)
- `man` – Show manual for a command
- `tldr` - Show summarised `man` for a command (*Requires install*)
- `grep` – Search for patterns in text
- `rg` - Faster grep (Requires install)
- `fd` – Faster search for files and directories (*Requires install*)
- `sed` – Stream editor for text transformation
- `awk` – Pattern scanning and text processing
- `sort` – Sort lines in text files
- `head` – Show the first lines of a file
- `tail` – Show the last lines of a file
- `xargs` – Build and execute commands from input
- `fzf` – Fuzzy finder for searching files and text (*Requires install*)
- `compgen -c` – List all available shell commands

### [[Bash Scripting]]/Shell Syntax / Operators
- `|` – Pipe output of one command into another
- `$( )` – Run a command in a subshell and capture output
- `>` – Redirect output to a file (overwrite)
- `>>` – Append output to a file
- `<` – Redirect file input into a command

## Nifty Command and Pipe Combos

As mentioned above, you can pipe command to each other using `|`. This can be used in interesting ways, if you find you use something often, save it to your bashrc or zshrc as an alias.

- `compgen -c | fzf | xargs man` - Fuzzy find any system command and get its manual
- 


See also:
- [[Terminal]]
- [[Bash Scripting]]