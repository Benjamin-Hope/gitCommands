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

The size of the commit matters. Commits should be performed as checkpoints. When a crucial section is developed thats when the commit should be performed, and not at the end of a feature.

Commits should be performed to store a state that we would like to record.

The messages on the commits should be helpful for other developers when reviewing the code.
Meaningful messages are always better than long descriptions.

The messages in the commits should be in the **present**. This is just a wording preference.

## Ignoring Files

We can inform git to ignore certain files. These usually are secure keys, or other private information. To store and hide these we can create lock files. Ideally, every developer should have a lock file.

To inform git which files we would like it to ignore we run the command `.gitignore`.
This will be in the root of our project. To inform it which files we would like it to ignore we can do:

`echo files/ > .gitignore`

In the command above we are adding the path of the file to the `gitignore` extension. We can include as many files and paths in this as want.

Despite git ignoring the files and the changes associated with it, we still need to stage the updates made to the `gitignore`file.

**Note**: Once a file has been committed, git tracks it, even if we include it afterwards in the ignore section.

We can check the files that git is tracking with the command `git ls-files`.

## Remove files or Directories

- To remove a file from the tracked files along with the staging area, we use the `git rm filename` command.

- To remove a file from the tracked files we use the `git rm --cached -r filename`.

**Note**: In the git documentation, the **index** refers to the tracking area.

After the previous change the commit still needs to be performed.

## Review code

We can also review the modifications performed to a code in git. The command `git diff --staged` will show us the changes performed to the files in the staged area. To check the changes in files that are not staged yet we run the command `git diff`.

Checking for differences in the code often times is hard to understand in the terminal. Therefor, visual tools are utilized. The most popular ones are:

- Kdiff3
- P4Merge
- WinMerge

We can set the VScode as out default diff tool with the command:

`git config --global diff.tool vscode`

Then we need to define how it will launch it:

`git config --global difftool.vscode.cmd "code --wait --diff $LOCAL $REMOTE"`

The command above tells what we want to open vscode and keep it open until it is closed and that we cant to have access to old and new copies of the files.

Now, for comparison instead of running the `git diff` we can run the `git difftool` to run the vscode diff session.
Similar to the previous method, if we do not specify anything else we will compare the unstaged changes. To compare the staged changes we need to run `git difftool --staged`.

## History

We can check the commit history by running the command `git log`. Which will give information about the previous commits performed.

The main branch or main line of work in git is called **Master**. And **HEAD** is a reference to the current branch, so we know in which branch we are working on.

We can have a short summary of the logs and commits by adding the `--oneline` option to the command such as,
`git log --oneline`.

### Commit detailed information

We can check more detailed information of the commits by running the command `git show [commit_id]`.

We can do this in another way. We can consider the last commit as **HEAD** and then specify how many commits we would like to go back. Here is an example:

`git show HEAD~2` In here we go 2 commits back.

## Remove files from staging

To remove a file form the staging area we use the command `git restore --staged [filename]`. If we would like to restore everything in the staging area we would use `.` instead of the filename.

To remove all the unstages files which git does not know here to get them from, since there no available information, we run the command `git clean`.

## Checkout

The checkout functionality is to get back to the previous progress of a commit we would use the following command:

`git checkout [commit_id]`

When we do the checkout we are in a different branch. We can think of this as different timelines.

## Associate git to github

To associate an existing git that we have created locally to a new repository on github we run the command:

`git remote add origin [link]`

**Note**: Commits are checkpoints that are present locally. To append this to the website (github) or any other remote environment we need to **push** it. To do t his we use the command:

`git push -u origin master`

## Creating branches

To creating branches we just need to duplicate a snapshot of the current state of the code. This means that we use the `git checkout -b [branch-name]`.

To push the new branch changes into the repository we would use the command:

`git push origin [branch-name]`

The above command will just publish the branch, not merge t hem.
To merge the branches we would do a **merge request**.

## Updating local repository

Our local repository representing our computer, might be outdated considering the code that other people push to the remote master. To update our local with these we would do a **pull request**. To do this we would run the command:

`git pull origin master`

## Merging

### What is Merging?

Merging combines the changes from one branch into another, typically from a feature branch into the `main` or `develop` branch. It creates a new "merge commit" that keeps the history of both branches.

### How to Merge a Branch

```bash
# Ensure you're on the target branch (e.g., main)
git checkout main

# Pull the latest changes
git pull origin main

# Merge the feature branch into main
git merge <feature_branch>

# Push the changes to the remote repository
git push origin main
```

## Rebasing

Rebasing moves or replays your branch’s commits on top of another branch instead of merging. This creates a linear commit history without merge commits.

```bash
# Switch to the feature branch
git checkout <feature_branch>

# Rebase it onto the latest main branch
git rebase main

```

If conflicts arise during rebasing we would do:

```bash
# Edit the conflicting files and stage them
git add <resolved_file>

# Continue rebasing
git rebase --continue
```

To abort a rebase and go back to the original state we would use:

`git rebase --abort`

**When to use rebasing?**

- When you want a clean commit history without merge commits.
- When working on private branches before pushing to remote.

## Merge Requests or (Pull Requests)

A Merge Request (MR) (or Pull Request (PR) in GitHub) is a request to merge changes from one branch into another. It allows for code review and collaboration before merging. The steps to do this are the following:
