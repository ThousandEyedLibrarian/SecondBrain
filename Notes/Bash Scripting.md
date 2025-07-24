
Firstly, always add `set -euo pipefail` to the beginning of your script after `#! /usr/bin/env/bash` for better script behaviour.

## Quick Start
1. Write your script sans `.sh` extension
2. Chuck it in `usr/local/bin` or `~/.local/bin`
	1. Really anywhere as long as that directory is in your `$PATH` environment  variable
3. Have fun, you can use the script as a terminal command now

Note: If the script is local to a project, save it with the .sh extension and keep it in the project directory.

## Useful Commands

| Command                          | Effect                                            |
| -------------------------------- | ------------------------------------------------- |
| `var=$(command)`                 | Set var to the output of command, e.g. `pwd`      |
| `diff <(ls ./v1) <(ls ./v2)`     | Feed the outputs of two commands to another       |
| `$((1+1))`                       | Arithmetic in the shell                           |
| `if [[ $val == "a" ]]; then`     | Start an if block on a single line                |
| `sleep 5`                        | Sleep x seconds                                   |
| `read -r name`                   | Read in user input to var name                    |
| `arr=(1 2 3 4)`                  | Set an array                                      |
| `for item in ./content/*.md; do` | Iterate using pattern matching                    |
| `for item in $(ls); do`          | Iterate using command result                      |
| `trap command signal`            | Run command when a given signal occurs, e.g. EXIT |
| `alias`                          | Set a system wide command alias                   |


See also:
- [[Command Line]]
- [[Terminal]]
- [Bash Scripting Tutorial for Beginners](https://linuxconfig.org/bash-scripting-tutorial-for-beginners)
- [Become a bash scripting pro - full course](https://www.youtube.com/watch?v=4ygaA_y1wvQå)