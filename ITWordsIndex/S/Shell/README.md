## How to find out which one your Mac is using.
Type the command into the terminal, and if it returns a number, it's the shell you're using.
```
echo $ZSH_VERSION
// using zsh

echo $BASH_VERSION
// using bash
```

# What is a shell?
> A user interface (interpreter between human and PC (kernel)) that stands between the OS and the application to convey user requests to the system.
A program that runs by entering commands, which are called variously **command prompt, terminal, terminal**.
There are several types of shells, including **sh, bash, csh, and zsh**.

## Features of shells
There are two types of shells: login shells and non-login shells.
A login shell is a shell that is applied when you log in to a UNIX-like OS.
A non-login shell is a shell that is applied arbitrarily after logging in to a UNIX-like OS.

## Difference between Bash and Zsh
These two incorporate the functions of other shells and have high performance.
### Bash.
The most commonly used shell, which is an extension to the oldest shell on UNIX, sh.
It does not need to be customized.
### Zsh.
A shell that is said to have taken the best parts of other shells (it has almost all the features of sh, bash, csh, and tcsh).
Customizable
Lightweight


***

[What is a shell, bash or zsh, which one does my Mac use?] (https://mykii.blog/what-is-shell-bash-and-zsh/)