# How to use Git and its Commands

## Table of contents

## Using Git

There are various environments where we can sue git:

- Command line (fastest and easiest)
- Code Editors and IDEs
- Graphical user Interfaces

## Configuring GIT

We can configure multiple parameters such as:

- name
- email
- Default Editor
- Line Endings
- ...

We can specify these also in different levels:

- System : Apply to all users of the computer
- Global : All repositories of the current user
- Local : Apply to the current repo

To define these we do the following:

`git config --global user.name "John Doe"`

`""` are needed in here in because the name contains a space, if we would set something like the email, this is not required.

`git config --global user.email myemail@gmail.com`

It ios always recommended to set the editor we would like to work in. TO set Visual Studio Code we do the following:

`git config --global core.editor "code --wait"`

**Note**: In order for the above to work we need to set VSCode in our path environment variables, so that we can call it from anywhere.

We can also write the following command to open our default editor and configure our settings:

`git config --global -e`

The definition of the end of lines is very important and OS dependent. On windows this is marked with `\n` and `\r`, which are Line feed and Carriage Return, respectively.

On linux and mac only the `\n` is required.

To set this we need to use `core.autocrlf`. If we are working on windows, this parameter needs to be set to true, on mac and linux it has to be set to input.

Windows: `git config --global core.autocrlf true`
Linux and Mac: `git config --global core.autocrlf input`

## Commands

### Initialize a repository

A syntax of the commands can be found in [Git commands Cheat Sheet](git.pdf).

To create a git repository, you can simply run `git init` in a specific folder location and it will initialize a git repo for us with some information in a hidden `.git` file.

This file is not to be edited, fut if you open it you can check some useful information in it. **If this file is removed, we are going to lose our git repository.**

### Git Workflow

When we create changes to the code, these can be stored in a area, separate from the main code called **staging area** here we can visualize all the changes that we did. Once we are happy with them we can take a **snapshot** and sent it over to the main algorithm to be integrated in.

To **add** the files to the **staging area** we use the command **git add file1 file2**, this will add the file 1 and file 2 ot the staging area.

After reviewing these stage files we can commit them with the command:

`git commit -m "commit message"`

As we can notice, we can insert messages within the commit to inform about the changes performed. This will permanently store the snapshot in the repository.

**Note**: When we performed a commit and perform new changes to the code, we are requited to add them back again to the staging area, because if not, the staging area will contain the old version, and not the updated one.

Each commit contains the following information:

- ID
- Message
- Date and time
- Author
- Complete snapshot

We can also have information of the status of the working area by running the command:

`git status`

This will inform about the commits, the tracked and the untracked files (staging).

If we write only the `git commit` without the rest, our default editor will open on which we can add a short description, a long description, comments and other information to the commit. To save the changes all we need to do is to close the windows.

## Best practices for Committing code

The size of the commit matters.
