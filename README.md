# git stash and run at host

*git-sarah* is a simple script that uses `git` and `ssh` to copy the
current state of your repository (including uncommitted changes) to a
remote computer and runs a command there.

A typical use case is compiling and/or testing your program on a more
powerful machine.

## Usage

Suppose you have a *program* that need to be compiled by running
`make` in the `build` directory. So on your local machine the program
can be compiled by:

    cd build
    make

To use `git-sarah` to compile the *program* on a *server*, prepare the
repository on the *server*:

    ssh me@server
    mkdir program_dir
    cd program_dir
    git init
    logout

Then compile the program by running:

    cd build
    git sarah me@server program_dir -- make

The absolute paths in the output of `make`, running on the *server*
will be modified to match your local computer, so that your editor/IDE
will be able to jump to the error locations reported by the compiler
(if any).

If you want to run more than a single command, e.g. a whole script,
but don't want to commit it to the repository, you can run the script
as follows:

    git sarah me@server program_dir -- sh < ./script.sh
