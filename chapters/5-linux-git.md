# Linux and Git Commands

The following sections list of the more commonly used Linux and Git
commands.

You will find them useful for the lesson on Version Control Systems.

Most of these commands have tons of options you will seldom use.
We'll cover some of the more frequently used ones here, but you can always
find out more by checking the command's documentation.

In Linux (and OS X), you can look up the documentation for a command with
`man` (manual).
For example, `man ls` opens the manual page for the `ls` command.

`man man` displays documentation for the `man` command itself!

## Some Conventions

In this cheatsheet, `<something>` indicates that `something` is a variable.
You should replace it with the thing you want the command to act on.

`<something ...>` means that the command can accept multiple arguments.
Each argument is separated by a space.

Useful options will be listed as sublists.

## Linux

* `ls <directory name>`: List directory contents.
If no directory is specified, list the contents of the current directory.
  * `-l`: displays listings in a long format.
  * `-a`: also displays hidden files.
* `pwd`: Get the name of the current working directory.
* `cd <directory name>`: Change working directory to `directory name`.
If no directory is specified, goes back to the home folder.
* `cat <filename ...>`: Con**CAT**enate and print files.
* `nano <filename ...>`: Open specified files with the nano text editor.
* `vim <filename ...>`: Open specified files with the vim text editor.
* `mv <source> <destination>`: **M**o**V**es file named `source` to `destination`.
  Also used for renaming files.
* `cp <source> <destination>`: **C**o**P**ies file named `source` to `destination`.
  * `-r`: If `source` is a directory, copies the directory and everything in it
  to `destination`.
* `rm <filename ...>`: **R**e**M**ove specified files.
  * `-r`: Removes directories and their contents.


## Git

Each command here is prefixed with `git`. They are subcommands which belong
to the main `git` command.

* `checkout <branch name>`: Switch to the specified branch.
  * `-b`: Create a new branch with that name.
  If the branch exists on the server, Git will automatically track the branch.
* `clone <URL> <directory name>`: Clone the repository into the specified directory.
  If `directory name` is not specified, a directory is automatically created.
* `add <filename ...>`: Tells Git you want to add these files to the next commit.
* `commit`: Creates a new commit which records your changes.
  * `-m "<commit message>"`: Specify a commit message. Quote marks are necessary.
* `mv <source> <destination>`: Tells Git you want to move or rename a file.
* `rm <filename ...>`: Removes file and tells Git.
* `pull <remote name> <branch name>`: Fetch changes from the server and integrate
them with your copy.
* `diff`: See the changes made so far.
  * `--staged`: See changes you've made after running `git add`.
* `status`: Show the status of the repository.

Git is a very powerful tool with many advanced features.
Should you wish to learn more, the entire [Pro Git](https://git-scm.com/book/en/v2)
book is available for free.

