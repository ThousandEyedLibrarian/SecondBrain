## Quick Start
1. Write your script sans `.sh` extension
2. Chuck it in `usr/local/bin` or `~/.local/bin`
	1. Really anywhere as long as that directory is in your `PATH` environment  variable
3. Have fun, you can use the script as a terminal command now

## Useful Commands

| Command                      | Effect                                       |
| ---------------------------- | -------------------------------------------- |
| `var=$(command)`             | Set var to the output of command, e.g. `pwd` |
| `diff <(ls ./v1) <(ls ./v2)` | Feed the outputs of two commands to another  |
| `$((1+1))`                   | Arithmetic in the shell                      |
| `if [[]]; then`              | Start an if block on a single line           |
|                              |                                              |


See also:
- [[Command Line]]
- [[Terminal]]
- [Bash Scripting Tutorial for Beginners](https://linuxconfig.org/bash-scripting-tutorial-for-beginners)