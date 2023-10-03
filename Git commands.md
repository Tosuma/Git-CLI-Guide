# Terminology

## General Command Line Interface (CLI)

### Folder Structure

Every folder has, besides the content, two hidden subjects; ``.`` and ``..``

``.`` is the current folder. Depending on how the command works it might be
interpreted as the content of the folder, e.g. the command ``git add <Path>``
adds the changes made in the path, if the path is ``.`` the command ``git add .``
would add all changes made in this current folder, which includes all file
changes in said folder.

``..`` is the folder above the current folder. It is often used with the command
``cd ..`` which changes the command line directory to the to directory above.


### Square Brackets

The square brackets ( ``[ ]`` ) indicate that the enclosed element
(parameter, value, or information) is **_optional_**.
You can choose one or more items or no items.
Do **not** type the square brackets themselves in the command line.


#### Examples:

``[global options]``

``[source language="arguments"][/source]``

``[destination arguments]``


### Angle Brackets

The angle brackets ( ``< >`` ) indicate that the enclosed element
(parameter, value, or information) is **_mandatory_**. You are required to
replace the text within the angle brackets with the appropriate information.
Do **not** type the angle brackets themselves in the command line.


#### Examples

``-f <set the File Name variable>``

``-printer <printer name>``

``-repeat <months> <days> <hours> <minutes>``

``date access <mm/dd/yyyy>``


### Ellipsis

The ellipsis symbol of three periods ( ``...`` ) means "and so on" and
indicates that the preceding element (parameter, value, or information) can be
repeated several times in a command line.


#### Examples

``-jobid <job id1, job id2, job id3,...>``

``[-exitcode <exit code 1>,<exit code2>,<exit code3> ...]``


### Pipe

The pipe symbol (vertical line) means "or" and indicates a choice within an element.
If two arguments are separated by the pipe symbol, you can select the element to
the left of the separator or the element to the right of the separator.
You cannot select both elements in a single use of the command.
Within square brackets, the choices are optional. Within angle brackets,
at least one choice is required.

#### Examples

``-ca_backup [-custom|-rotation|-gfsrotation]``

``-excludeday <Sun|Mon|Tue|Wed|Thu|Fri|Sat>``

``-runjob <start|stop>``


### Curly Brackets

The curly brackets ( ``{ } `` ) indicates a set of required items, however,
you must choose one of the elements. The elements in the curly brackets are
seperated by the pipe operator.
Do **not** type the braces themself in the command line.


#### Examples

``{FILE_1 | FILE_2}``

``{--source=CLOUD_SOURCE --source-url=SOURCE_URL | --bucket=BUCKET [--source=LOCAL_SOURCE]}``


## Git

### Git

An open source, distributed version-control system.


### GitHub/GitLab

A platform for hosting and collaborating on Git repositories.


### Fork

A copy of a repository on GitHub owned by a different user.


### Branch

A lightweight movable pointer to a commit.


### Clone

A local version of a repository, including all commits and branches.


### Remote

The _remote_ is the branch which is in the cloud, e.g. GitHub/GitLab, hence remote.


### Local

The _local_ is branch which is locally on the computer.
This can be deleted without deleting the [remote](#remote) in the cloud.


### Working tree

The Working Tree in Git is a directory (and its files and subdirectory) on your
file system that is associated with a repository. 


### Commit

A _commit_ is a snapshot of the project's currently staged changes.
Committed snapshots can be thought of as "safe" versions of a project - Git will
never change them unless you explicitly ask it to.


### Stage

To stage af file or folder means that the subject has been added to the commit.


### Unstage

To unstage a file or folder means that the subject has been removed from the commit.


### Pull Request

A place to compare and discuss the differences introduced on a branch with
reviews, comments, integrated tests, and more.


### HEAD

Representing your current working directory.
Can generally be thought of the main/master branch.


# Basic Git Commands

## Get a reposetory on pc

```
git clone <repo link>
```

The ``git clone`` command lets you make a copy of a repo from some git service,
e.g. GitHub or GitLab.

_Note_: When executing the command the repo will be placed in your current location.

### Example

``git clone https://github.com/Tosuma/AAU-Latex-Template-English.git``- will
clone the repo 'AAU-Latex-Template-English' to your computer.


## Get status of your local / see changes

```
git status
```

This will give you a status of current [working tree](#working-tree). Here you
will be able to see the files which has had changes or have been added since the
last commit. You will also be able to see the files which has been [staged](#stage).


## [Stage](#stage) files to commit

```
git add <Path>
```

This command stages a file or folder to the commit.


### Example

``git add .`` - adds all changes made to the commit.
For more information [go to here](#folder-structure).

``git add ./API/API-documentation.md`` - adds the file 'API-documentation.md'
located in the folder 'API' to the commit.


## [Unstage](#unstage) files from commit

```
git restore --staged <Path>
```

The given path (file or folder) will be unstaged from the commit.
However, it is rare that it is used.

**NB:** This command is experimental, the behavior may change.


### Example

``git restore --staged ./API/API-documentation.md`` - removes the file
'API-documentation.md' located in the folder 'API' from the commit.

``git restore --staged .`` - removes all files and folders from the commit.
For more information [go to here](#folder-structure).


## Make commit

```
git commit [-m <message>]
```

This command commits all stages made.

It has the optional argument ``-m <message>``, which is the commit message - this
is more often than not included when making commits.
The message should be enclosed by single or double qoutes to make it a string.


### Example

``git commit -m "ADDDED: API-documentation.md"`` - commits the stages with the
message 'ADDDED: API-documentation.md'.


## Undo a commit you have made **_before_** push

```
git reset [--soft | --hard] [HEAD<~number>]
```

This command will let you undo a commit **_before_** it has been pushed to the
remote. It will still keep the changes you have made, but remember to commit the
changes you need! Use [``git status``](#get-status-of-your-local) to see the
changes which has been made.

The number in ``~number`` is the amount of commits you want to undo, which gives
you the option to undo multiple commits.

The ``--hard`` tag should be **_used with causion_** since it will remove all
changes - i.e. it destroys the changes made in the commits which are undone.

The ``--soft`` tag will leave your changes in the index, meaning that you can
make a commit immediately without doing ``git add``.


### Example

``git reset --hard HEAD~1`` - undos the latest commit and removes all changes
from said commit.

``git reset HEAD~2`` - undos the 2 latest commits and keeps the changes, however
they are not stages for a new commit.

``git reset --soft HEAD~1`` - undo the latest commit and keeps the changes where
the changes are staged and ready for a new commit.


## Push commits to the [remote](#remote)

```
git push [-u] [<repo_dst> <repo_src>]
```

This command updates the [remote](#remote) with the [commits](#commit) from the
specified [branch](#branch).


### Example

``git push`` - pushes the commits from the [local](#local) to the current branch.

``git push origin api-documentation`` - pushes the commits from the branch
'api-documentation' to origin. **NB**: This is a bad practise, 
use [pull requests](#pull-request) instead.


``git push -u origin my-new-branch``


## Pull the commits from the [remote](#remote)

```
git pull
```




## Go to another branch

```
git checkout
```


# Useful Commands

## Store Login Credentials

```
git config credential.helper store
```

This command will store the last credentials entered.


## Delete a branch from the local (locally on computer)

```
git branch -d <branch_name>
```

This command will delete the local branch, but not from the remote.


## Delete a branch from the remote (branch)

```
git push <remote_name> --delete <branch_name>
```

This command will delete the branch from the remote, but not from the local.
The ```remote_name``` will likely have to be ```origin```.


## Fetch general updates

```
git fetch
```

This command will fetch the recent changes from the cloud (like new branches or deleted branches) and print them.

Include the tag ```--prune``` or ```-p``` to prune (delete) any branches which has been deleted on the remote.


## See all branches

```
git branch <-r/-a>
```

This command will show all of the branches which can be checked out to. 

The ```-r``` tag will just show all of the branches.

The ```-a``` tag will show all of the branches as well as the branches which you are currently on and the others which is on the local.


## See local branch

```
git branch
```

This command will show all of the local branches and specify which is checked out to.


## See files which has been changed

```
git diff
```

This command will show all of the files which has changed and what has changed in them.

Include the tag ```--name-only``` to only see the names of the files.


## Discard changes to a specific file

This command will reset the specific file back to what is on the current remote.

```
git checkout -- <file_path>
```

The tag ``--`` is to make sure that git knows it is a file.


## Discard all changes made on branch

This command will discard all changes made, and reset back to what is on the current remote.

```
git checkout .
```


## Get graph of git commits

```
git log --all --decorate --oneline --graph
```