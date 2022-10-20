# Version control with GIT

## Repositories

A git repository is any directory which has been initialised by git, usually either with `git clone` or `git init`. It contains a hidden sub-directory `.git`, which contains the entire history of every other file and directory in the repository, except those files and directories which git has been told explicitly to ignore (see `.gitignore`).

You never deal with the contents of `.git` directly. Rather, you use various git commands such as `git checkout` and `git commit`, leaving git itself to handle the contents of that `.git` directory.

A respository can exist on a remote host such as Github, and/or on a local workstation. There is usually one repsoitory instance which is considered to be the authoritative "origin", to and from which users "push" and "pull" changes.

To create a local clone of a remote repository:

    git clone <repository_url>

To clone a Github repository, use the URL provided by Github's web interface. This file is in repository `/cabwood/aphelion_training` on Github, and that repository can be cloned with:

    git clone https://github.com/cabwood/aphelion_training.git

This URL uses HTTPS to communicate with Github, and will require manual authentication each time you "push". To avoid this requirement, follow the SSH key generation steps below, and use SSH instead

    git clone git@github.com:cabwood/aphelion_training.git

## Branches

A repository is a collection of "branches". The main branch is usually called "master" (or "main" on Github).

Each branch represents a named set of changes to files and directories in the repository. Branches can be used to create additional "release versions", such as alpha and beta test versions, release candidate versions, or final production versions. Most often branches will be created to try out ideas and changes, and when those changes are acceptable, they eventually get "merged" into the main branch.

To see a list of branches in your local repository, first ensure the PWD is somewhere within the repository tree (using `cd`, if necessary), then:

    git branch

To create a new branch stemming from the current branch use `git checkout` with the `-b` flag:

    git checkout -b my_new_branch

To delete a branch:

    git branch -d my_new_branch


## Staging

When you make changes to any file or directory within a git repository, those changes will be noticed by git. To see what files have changed since the last "checkout":

    git status

"Staging" is the process of telling git which of those changed files are to be included in the next "commit" operation. The command `git status` shows you which files are staged for commit (usually shown in green), and which files are not (red).

To stage a file for commit, the command is:

    git add path/to/file

To stage all changed files:

    git add .

## Commiting

To update the current branch with all staged files and directories:

    git commit

This will open an editor (in Ubuntu distributions. that's usually nano, by default) where you type a description of the changes. When the file is saved and the editor closed, the commit operation will be performed.

To avoid using the editor, you may use the `-m` option of the `git commit` command to specify a description on the command line:

    git commit -m "Added PayPal option to payment module"

You may view a log of the history of commits of the current branch with:

    git log

## Push and pull

All commits you perform are in the local repository only, and are not yet present at the remote origin. To update the remote origin repository with all committed changes:

    git push

If the branch you are trying to push does not exist in the remote repository, this will fail. You can only push branches which exist both locally and remotely.

It's possible that other contributors to the repository have committed (ans pushed) changes, meaning that your own local clone of the repository is out of date. To bring files in your local repository up to date:

    git pull

## Switching branches

You may create a new branch to implement and test changes, before merging those changes into the main branch. To do this, use the `-b` option of the `git checkout` command, followed by a meaningful name for the new branch:

    git checkout -b paypal_payment_option

This means that there may be several branches present locally, which may be listed as follows:

    git branch

You can switch between those branches, making any one "current" using `git checkout` *without* the `-b`:

    git checkout main
    git checkout paypal_payment_option
    git checkout beta

This can fail if there are unstaged and uncommited files in the current branch, so you may have to follow the staging (`git add`) and commit (`git commit`) procedure before switching branches.

## Merging

If you have created a new branch, that doesn't exist at the remote origin, you can't "push" it. You can only push branches that exist remotely.

So, if you are currently in branch "paypay_payment_option", and you wish to incorporate changes made in this branch to the "main" branch, you must merge branch "paypal_payment_options" into branch "main". First make sure there are no unstaged or uncommited files in "paypal_payment_option"

    git checkout main
    git merge paypal_payment_option

Then, optionally, you may update the remote repository's "main" branch too:

    git push

## Workflow

In summary, the workflow when using git might look like this:

1. Clone or init a repsository (`git clone` or `git init`)
  1. Make sure main branch is up to date (`git pull`)
  1. Create a new branch for implementing and testing some new feature (`git checkout -b name_of_branch`)
    2. As often as required:
      - Modify, create and delete files as required
      - stage changes (`git add`)
      - commit changes (`git commit`)
    3. Merge branch into main (ie. `git checkout main` then `git merge name_of_branch`)
  2. Push merged changes in main branch to the remote origin (`git push`)

## Using SSH with github.com

Git can use different protocols to communicate during "push" and "pull" operations, one of which is SSH. To avoid having to authenticate with a username and password each time a push or pull occurs to/from a remote repository like Github, we can use SSH public key authentication, but this requires that a public/private key pair exist on the client workstation.

There's a hidden directory in the user's home directory called `.ssh`, which contains two files:

    id_rsa
    id_rsa.pub

If they exist already, then they do not need to be created. Otherwise they may be created with:

    ssh-keygen

You will be prompted for a password. Since the objective is to enable SSH communications *without* having to type a password each time, leave this password blank.

The file `id_rsa` is a private key, and must never be shared with anyone. The other file, `id_rsa.pub` is public, intended to be shared with other users and systems. To view the contents of this file:

    cat id_rsa.pub

This output can be shared with any service that uses SSH for communication and authentication, such as Github. Subsequently, git push/pull operations can use SSH without having to manually authenticate each time.

