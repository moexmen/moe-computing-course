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

* `ls <directory_name>`: **L**i**S**t directory contents.
If no directory is specified, list the contents of the current directory.
  * `-l`: displays listings in a long format.
  * `-a`: also displays hidden files.
* `pwd`: Get the name of the current working directory.
* `cd <directory_name>`: Change working directory to `directory_name`.
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

* `git checkout <branch name>`: Switch to the specified branch.
  * `-b`: Create a new branch with that name.
  If the branch exists on the server, Git will automatically track the branch.
* `git clone <URL> <directory_name>`: Clone the repository into the specified directory.
  If `directory_name` is not specified, a directory is automatically created.
* `git add <filename ...>`: Tells Git you want to add these files to the next commit.
* `git commit`: Creates a new commit which records your changes.
  * `-m "<commit message>"`: Specify a commit message. Quote marks are necessary.
* `git mv <source> <destination>`: Tells Git you want to move or rename a file.
* `git rm <filename ...>`: Removes file and tells Git.
* `git pull <remote name> <branch name>`: Fetch changes from the server and integrate
them with your copy.
* `git push <remote name> <branch name>`: Push your changes to the server.
  Prelude to creating a pull request.
* `git diff`: See the changes made so far.
  * `--staged`: See changes you've made after running `git add`.
* `git status`: Show the status of the repository.

Git is a very powerful tool with many advanced features.
Should you wish to learn more, the entire [Pro Git](https://git-scm.com/book/en/v2)
book is available for free.

### Git Workflow

These steps and terms are specific to GitHub but competing products pretty much
do the same thing, except with different names.

#### Setup Steps

1. Fork the repository.
1. Clone it to your computer.

  `git clone <your-url>`
1. Set the original repository as and upstream remote so you can sync changes to your own copy.

  `git remote add upstream <original-url>`

#### Development Cycle

1. Create a new branch to work on.

  `git checkout -b <branch-name>`

1. Make your changes in logical chunks.
  Many small commits will make your history hard to read.
  Large commits make it hard to debug if necessary.

1. Add your changes to the staging area.

  `git add <filenames ...>`

1. Create a new commit of those changes.

  `git commit -m "<commit-message>"`

1. Repeat the 3 steps above until you are done with the work for your branch.

1. Push the branch to your forked repository.

  `git push origin <branch-name>`

1. Go to the main repository on GitHub and create a pull request.

1. When the pull request has been merged, sync your local copy.
  This will also pull in changes from other people.

  ```
  git checkout master
  git pull upstream master
  ```

1. Keep your forked repository in sync with the original.

  `git push origin master`

#### Additional Documentation

Related links to GitHub's documentation.

1. [Fork a Repo](https://help.github.com/articles/fork-a-repo/)
1. [Syncing a fork](https://help.github.com/articles/syncing-a-fork/)
