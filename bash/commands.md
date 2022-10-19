# ls

List files in the present working directory (PWD):

    ls

List files with addition information, such as size, ownership, permissions etc ("long" listing):

    ls -l

List all files, including hidden ones (which are prefixed with '`.`')

    ls -a

Most Linux distributions have a command `ll` which is an alias for `ls -a -l`. To list all files, including hidden ones, in the "long" format:

    ll

# Combining flags

Most commnands permit you to concatenate several single-character "flags", or "options", or (as they are referred to in Windows) "switches" into a single compouud flag. The following two commands do the same thing:

    ls -a -l
    ls -al

# Present woring directory

The "present working directory" (PWD) is the directory where commands you type will operate. For example, the command `ls` lists the files in the PWD, and `mkdir` will create a directory in the PWD, and so on.

To display the present working directory, the command is:

`pwd`


## Changing the PWD

Use the `cd` command ("change directory") to change the PWD. To "move into" the root directory:

`cd /`

To change the PWD to your home directory, use `cd` with no arguments:

`cd`

## Parent & current directory

Every directory contains two hidden directories:

 - `.` represents the PWD. The command `cd .` does nothing!
 - `..` represents the parent of the PWD. The command `cd ..` "moves you up" into (sets the PWD to) the PWD's parent.

## Absolute and relative paths

If a file path begins with `/`, it is assumed to begin at the root. With no `/` at the beginning, a path is assumed to begin in the PWD.

For example, if the present working directory is `/home/simon`:

 - `ls /etc` will list files in the directory named `etc` which is located in the root directory.
 - `ls etc` will list files in the directory `/home/simon/etc`
 - `cd Documents/thesis` will attempt to set the PWD to `/home/simon/Documents/thesis`
 - `cd /Documents/thesis` will fail because there's no directory called `Documents` in the root

# Escaping file names

The linux command line interpreter assumes that each space character in your commands separates arguments. If your file or directory name contains a space, you must either escape the space using a backslash `\`, or enclose the name in quotes:

 - `ls My thesis` will attempt to list the contents of two distinct directories `My` and `thesis`
 - `ls My\ thesis` will treat the space as part of the same argument, listing the contents of the directory named "My thesis"
 - `ls "My thesis"` will treat the text inside quotation marks as a single argument, treating the space as part of the file/directory name

# Autocompletion

Pressing the `TAB` key requests the interpreter to attempt to find the best matching command or file/directory name, and "type" it for you. For example, typing `pyt<TAB>` will cause the interpreter to autocomplete the command to become `python3 `.

If there are multiple matches, pressing `TAB` twice will display a list of possible options:

~~~
py<TAB><TAB>
py3clean           pydoc3             pygettext3.10      python3.10-config
py3compile         pydoc3.10          python3            python3-config
py3versions        pygettext3         python3.10
~~~

If you have a file named `My thesis` in the PWD, then typing `ls My<TAB>` will cause the inpterpreter to fill in the rest: `ls My\ thesis`

# Command history

Using the up and down arrow keys on the keyboard allows you to cycle up and down through the entire history of commands that you have entered. This is useful if you wish to repeat a command, or if you have made a mistake in a command, and wish to try again. Press the up/down arrows until you see the command you wish to repeat/edit, make any necessary changes to the command, and press `ENTER` again to execute it.

# man

Most Linux commands have an information manual that can be viewed using the `man` command. These "man-pages" can be viewed with the `man` command:

 - `man ls` will display the reference manual for the command `ls`, which explains all the flags and options that you may use with it.

 Man pages are displayed using the `less` application, a simple text viewer in which you may navigate up and down the document using the arrow and page-up/down keys. To quit the viewer, and return to the command line, press the `q` key.

# mkdir & rmdir

Command `mkdir` will create a new, empty (excpt for `.` and `..`) directory. If the path you specify is relative (*not* prefixed with `/`) then the directory is created in the PWD.

 - `mkdir training` will create a directory called `training` in the PWD
 - `mkdir /home/simon/Documents/training` will create a sub-directory `training` in directory `/home/simon/Documents`

 Command `rmdir` is used to delete directories:

 - `rmdir training` will delete the directory `training` which exists in the PWD.
 - `rmdir /home/simon/Documents/training` will delete directory `training` from its parent directory `/home/simon/Documents`

`rmdir`  will fail if the directory being deleted is not empty. If you wish to use `rmdir` to remove a directory, you must empty it first.

# rm

Command `rm` is used to delete a file, or files.

 - `rm thesis` will delete the file `thesis` which exists in the PWD.
 - `rm /home/simon/Documents/thesis` will delete file `thesis` from directory `/home/simon/Documents`

`rm` may also be used to delete a directory (along with its contents). Where `rmdir` will fail if the directory being deleted is not empty, `rm` can succeed when used with the `-r` flag, which will recursively remove all files within, and all sub-directories, and their sub-files and sub-directories and so on. Usually the interpreter will prompt for confirmation of each individual deletion, but this can be circumvented with the `-f` flag:

`rm -fr years_of_hard_work` will delete directory `years_of_hard_work` from the PWD. It won't ask for confirmation, it will just do it, and you will lose years_of_hard_work forever, unless you have backed it up somewhere.
`rm -fr /home/simon/years_of_hard_work` will delete directory `years_of_hard_work` from its parent directory `/home/simon`.

***Use `rm -fr` with extreme caution***. The commands `rmdir` and `rm` have no concept of a "recycle bin", such as you'd find in Microsoft Windows. Consequently if you delete a file or directory using those commands, they are gone forever. However, most Linux distributions with a graphical desktop environment *do* have a "trash can" feature, and files/directories deleted using the GUI *can* (usually) be recovered.

