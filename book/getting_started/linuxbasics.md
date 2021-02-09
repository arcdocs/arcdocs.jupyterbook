# Linux basics

The HPC systems at Leeds run on a variant of the Linux operating system and we interact with the system using a command-line interface (CLI) rather than a graphical user interface (GUI) which we often use on personal computers.
The command line allows you to interact with the operating system through a series of commands that we type in and are executed after we hit the Enter key.
| The ARC4 command line after logging in |
| ----------------------------------------------------- |
| ![ARC4 command line after logging in with MobaXTerm](../assets/img/logon/mobaSSH_4.png) |

## Linux Tutorial

If you're totally new to Linux and the command line strongly encourage you to attend our training sessions [HPC0: Introduction to Linux](https://arc.leeds.ac.uk/training/courses/hpc0/) and [HPC1: Introduction to HPC at Leeds](https://arc.leeds.ac.uk/training/courses/hpc1/). These run throughout the year and provide a good basic introduction to both Linux and how to use the HPC at Leeds. If you'd like to learn more about Linux and the command line in your own time we also strongly recommend the Software Carpentries lesson on the [Unix shell](http://swcarpentry.github.io/shell-novice/) which offers a step-by-step tutorial you can take at your own pace.

## Some helpful shell commands

Commands in the terminal (or shell) follow a common pattern:

```bash
command <options prefixed with - or --> <arguments>
```

See below for a table of commonly used shell commands and a description of what they do. You can always find out more details by a command by googling it or using the `man` command to open the manual page for a specific command for instance:

```bash
man ls
```

Will return the manual page for the `ls` function including addition options that can be used and a more expansive description of its use. You can leave the manual page by pressing the Q key to return to the terminal.

| Command | Description                                                     |
| ------- | --------------------------------------------------------------- |
| `ls`    | List the contents of a directory                                |
| `cd`    | Change directory                                                |
| `pwd`   | Print the working (current) directory                           |
| `mkdir` | Make a new directory (folder)                                   |
| `mv`    | Move a file or directory (can be used to rename files)          |
| `cp`    | Copy a file or directory (using the option `cp -r`)             |
| `head`  | Show the first 10 lines of a file                               |
| `tail`  | Show the last 10 lines of a file                                |
| `less`  | Open a file into a reader view (Press Q to exit)                |
| `cat`   | Concatenate files and print to terminal (via standard output)   |
| `rm`    | Permanently remove file or directory (using the option `rm -r`) |
| `unzip` | Unpack a zip file                                               |
| `tar`   | Used to create and unpack tar archive files                     |
| `nano`  | Open a basic text editor program                                |
