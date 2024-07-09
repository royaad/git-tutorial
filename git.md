# Git

In this document, we delve into various Git commands and their functionalities. You'll notice that commands performing the same actions are presented alongside each other, with one version highlighted as a comment to emphasize its shorter form.

Let's explore the world of Git commands together!

## Table of Contents

1. [Github](#1-github)
2. [Git Basics](#2-git-basics)
3. [Git Configuration](#3-git-configuration)
4. [Git Cloning](#4-git-cloning)
5. [SSH (Secure Shell)](#5-ssh-secure-shell)
6. [Initializing and Pushing a Local Repository](#6-initializing-and-pushing-a-local-repository)

## 1. Github

### 1.1. Insights/Network

### 1.2. Commits

### 1.3. Default Branch Name

To establish the default branch name through the git GUI, navigate to Settings → Repositories. Subsequently, input the desired default branch name for your new personal repositories.

## 2. `git` Basics

Let's explore some fundamental `git` commands to kickstart our journey.

To display the version of `git`, use the following command:

```bash
git --version
```

For a comprehensive list of `git` commands:

```bash
git help
```

To get help on a specific command, such as `config`, you can use any of the following:

```bash
git -h config
# or
# git --help config
# git help config
```

Additionally, to open a help page in the web browser for terminal assistance, you can use:

```bash
git config -h
```

## 3. `git` Configuration

`git config` is used to configure various aspects of Git. It has three levels:

- Global: Configuration settings that apply globally to the user's system.
- System: Configuration settings that apply to every user on the system and all repositories.
- Local: Configuration settings that apply only to the current repository.

### Getting Configuration Information

- To obtain a list of git configurations:

  ```bash
  git config -l
  # or
  # git config --list
  ```

- For only the global, system, or local configuration list:

  ```bash
  git config --global -l
  git config --system -l
  git config --local -l
  ```

- To show the origin/source of each configuration:

  ```bash
  git config -l --show-origin
  ```

- To retrieve a specific value from git config:

  ```bash
  git config user.name
  # or
  # git config --get user.name
  ```

### Configuring Git

It is usually a good practice to configure the global configs of git as it offers ease of use for later.

- Configure username globally:

  ```bash
  git config --global user.name "royaad"
  # or
  # git config --global --set user.name "royaad"
  ```

- Configure user email globally:

  ```bash
  git config --global user.email "royaad@live.com"
  ```

- Set the default branch name to main:

  ```bash
  git config --global init.defaultBranch main
  ```

- Enable reuse recorded resolution:

  ```bash
  git config --global rerere.enabled true
  ```

- Configure better branches display:

  ```bash
  git config --global column.ui auto
  git config --global column.branch plain
  git config --global branch.sort -committerdate
  ```

- Configure the init default branch to "main":

  ```bash
  git config --global init.defaultBranch main
  ```

- Access global config editor (vim editor / press `i` to insert new lines, `:q!` to quit without saving, and `:wq` to save and quit):

  ```bash
  git config --global --edit
  ```

- In case we need to remove/unset a variable (e.g. user email) globally:

  ```bash
  git config --global --unset user.email
  ```

### Customizing Git

We can customize git to look better or create shortcut commands for easier use.

- Example of assigning custom colors for status:

  ```plaintext
  [color "status"]
    added = green
    changed = yellow
    untracked = red
  ```

- Example of assigning custom colors for branches:

  ```plaintext
  [color "branch"]
    remote = yellow
  ```

- Setup an alias globally:

  ```bash
  git config --global alias.st status
  git config --global alias.comess "commit -m"
  ```

- For more useful git aliases, check [this link](https://opensource.com/article/20/11/git-aliases). This addition provides a link to more useful git aliases.

### Config CRLF

Windows, Linux, and Mac use different control characters to mark a line break in a text file. Windows uses two characters CR LF; Unix (and macOS starting with Mac OS X 10.0) only uses LF; and the classic Mac OS (before 10.0) used CR. By default, git is set to auto-correct the CRLF differences. We can check this by typing

```bash
git config --system -l
```

, and we'll see the option `core.autocrlf=true`. This will lead to a warning message: `warning: LF will be replaced by CRLF`. To suppress these messages, we can set `autocrlf` to false by typing:

```bash
git config --global core.autocrlf false
```

For further readings, refer to [link 1](https://stackoverflow.com/questions/1552749/difference-between-cr-lf-lf-and-cr-line-break-types) and [link 2](https://stackoverflow.com/questions/17628305/windows-git-warning-lf-will-be-replaced-by-crlf-is-that-warning-tail-backwar).

## 4. `git` Cloning

### Cloning a remote repo

1. **Initialize the Command Line Interface**: Navigate to the desired directory where the repository is to be cloned. This can be accomplished by launching the command prompt and utilizing the `cd` command to reach the target directory.

2. **Repository Cloning**: Execute the cloning process in the local repository by employing the following command:

```bash
git clone <repository_URL>
```

Please substitute `<repository_URL>` with the URL of your specific repository.

**Note**: Upon successful cloning of a repository, the origin and the branch name are automatically configured in the local repository. This is a standard feature of Git's cloning operation. It ensures that the local repository maintains a link to the remote repository, facilitating subsequent fetch, pull, and push operations.

### Advanced cloning

1. **Cloning up to a certain depth**:

   ```bash
   git clone --depth=1 [https]
   ```

   The command creates a shallow clone with a history truncated to the specified number of revisions. In this case, `--depth=1` creates a clone with only the latest commit. This is useful when working with large repositories where you only need the most recent changes.

2. **Fetching more depth**:

   If you initially cloned a repository with a limited depth, but later need more of the history, you can use

   ```bash
   git fetch --depth=100
   ```

   This command fetches more commits from the remote repository, extending the history to the specified number of commits. In this case, `--depth=100` fetches the latest 100 commits.

3. **Downloading all remaining history**:

   If you decide that you need the complete history, you can use

   ```bash
   git fetch --unshallow
   ```

   This command fetches all the remaining commits from the remote repository, effectively converting the shallow clone into a complete clone.

## 5. SSH (Secure Shell)

**Secure Shell (SSH)** is a cryptographic network protocol that allows secure remote login from one computer to another over an insecure network. SSH provides strong password and public key authentication, secure data communications, and data integrity. It is widely used by network administrators for managing systems and applications remotely, allowing them to log into another computer over a network, execute commands, and move files from one computer to another.

When _Git_ is used over _SSH_, the data transfer happens over a secure channel. No plaintext data, including passwords, is ever transferred. This is why _SSH_ is the recommended method for interacting with remote _Git_ repositories.

Now, let's proceed with the instructions:

1. **SSH Verification**: Validate the SSH connection by executing the `ssh` command. This will initiate an SSH client program and establish secure shell sessions on remote machines.

2. **SSH Key Generation**: Generate an SSH key using the RSA encryption algorithm with a key size of 4096 bits. This can be accomplished by executing the following command:

   ```bash
   ssh-keygen -t rsa -b 4096 -C "royaad@live.com"
   ```

   Please replace `"royaad@live.com"` with your specific email address.

3. **Binding to GitHub**: Establish a connection to GitHub from the local Git repository. This can be done by executing the following command:

   ```bash
   ssh -T git@github.com
   ```

   This command attempts to SSH to GitHub, verifying that your machine has been correctly configured with your personal identity SSH key. If the connection is successful, you will see a message indicating that you've successfully authenticated. However, GitHub does not provide shell access.

Please note that these instructions assume that you have already installed and configured Git and SSH on your machine. If not, you will need to do so before proceeding. Additionally, ensure that you replace `"royaad@live.com"` and `"git@github.com"` with your specific email address and GitHub account, respectively.

## 6. Initializing and Pushing a Local Repository

### 6.1. Repository Initialization

The inception of any local repository begins with its initialization. This is accomplished by executing the `git init` command.

1. Navigate to the desired directory:

   ```bash
   cd <path-to-directory>
   ```

2. Initialize the local repository:

   ```bash
   git init
   ```

### 6.2. Adding a Remote Repository

Upon initialization of the local repository, it is generally advisable to establish a connection with a remote repository.

1. Navigate to github.com and create a **new, empty** repository.
2. Link the local repository to the remote one:

   ```bash
   git remote add origin [https]
   ```

3. Verify the remote repository:

   ```bash
   git remote -v
   ```

**Note:** A local repository can be linked to multiple remote repositories. To add another remote repository named 'colab', execute:

```bash
git remote add colab [https]
```

In the absence of a specified repository, 'origin' serves as the default.

### 6.3. Staging Files for Commit

Once the repository is initialized, new and modified files must be staged prior to being committed.

- To stage all files, execute:

  ```bash
  git add .
  # or
  # git add \*
  ```

- More often, specific files are staged:

  ```bash
  git add <filename>
  ```

- To remove a specific file from staging:

  ```bash
  git reset head <file>
  # or
  # git restore --staged index.html
  ```

### 6.4. Committing Changes

After staging, the files should be committed. The commit operation creates a permanent snapshot of the repository with a unique SHA number, enabling access to any specific state of the repository.

- To commit staged files:

  ```bash
  git commit -m "commit message"
  ```

- If a commit needs to be modified, the `--amend` flag can be used. For example:

  - To amend the last commit message:

    ```bash
    git commit --amend -m "new commit message"
    ```

  - To add more changes to the last commit:

    ```bash
    git add forgotten-file.txt
    git commit --amend --no-edit
    ```

- To undo the last commit while preserving the changes in the working directory for further editing:

  ```bash
  git reset --soft HEAD~1
  ```

### 6.5. Pushing Changes to Remote

After committing the changes to the local repository, they must be pushed to the remote repository to synchronize the two.

- The standard syntax to push a commit to the remote repository is:

  ```bash
  git push [remote] [from]:[to]
  ```

  However, more often we use:

  ```bash
  git push [remote] [to]
  ```

  Or more specifically:

  ```bash
  git push origin master
  ```

  Or simply:

  ```bash
  git push
  ```

  By default, the remote repository and branch are set to 'origin' and 'master' or 'main', respectively.

- When pushing for the first time, if the branch doesn’t exist on the remote repository, it must be set up:

  ```bash
  git push -u origin master
  # or
  # git push --set-upstream origin master
  ```

- To push all matching branches:

  ```bash
  git push origin :
  ```

- Specific branches can be pushed to sub-branches of other repositories:

  ```bash
  git push colab master:satellite/master dev:satellite/dev
  ```

  In this case, the local 'master' branch is pushed to the 'satellite/master' branch of the 'colab' remote repository, and the local 'dev' branch is pushed to the 'satellite/dev' branch of the same remote repository.

For more examples of push operations, refer to the [official Git documentation](https://git-scm.com/docs/git-push#_examples).

### 6.6. Comprehensive Initialization and Push Example

#### Scenario: Empty Remote Repository

1. Open a command prompt in the directory to be pushed.
2. Initialize the directory as a local repository:

   ```bash
   git init
   ```

3. Stage the files for their first commit:

   ```bash
   git add .
   ```

4. Check the status:

   ```bash
   git status
   ```

5. Commit the files:

   ```bash
   git commit -m "first commit"
   ```

6. Add the URL of the repository (only the first time):

   ```bash
   git remote add origin [https]
   ```

7. Push the repository:

   ```bash
   git push -u origin master
   # the -u flag is used only the first time
   ```

**Note:** It is generally good practice to pull changes before pushing. The pull operation will be discussed in a subsequent section.

#### Scenario: Non-Empty Remote Repository

Steps 1-6 are the same as in the previous scenario.

7. Since the remote repository is not empty, the remote files should be pulled first. However, this is not a normal pull operation since the two repositories do not share a related history. Care must be taken to ensure that the pull operation does not result in a loss of files. To pull the repository:

   ```bash
      git pull --allow-unrelated-histories origin

   ```

8. Push the repository (the 'master' branch is already set, so the '-u' flag is not needed):

   ```bash
   git push origin master
   ```

## 7. Git Branching

Check the list of existing branches.
git branch or git branch -l or git branch --list
We create a branch, named ‘alpha’ as example, using
git branch alpha
N.B. The files of the master branch are automatically copied to the alpha branch. In general the files of the branch which was originally checked-out when the new branch is created are copied. For example, if we change the files in the alpha branch and now, being in the alpha branch, type git branch beta, the beta branch will have the same files as the alpha branch.
We switch to that branch by typing
git checkout alpha
N.B. git manages the files automatically when switching branches.
We can equally create and switch to a branch in one command
git checkout -b beta
We can delete a fully merged branch by using the -d flag
git branch -d beta
And, we can force delete a branch (even if not merged) by using the -D flag
git branch -D beta

## Git branch

We can check the local branches by using
git branch
To check remote branches, we use
git branch -r
And to check both local and remote, we have
git branch -a
And we can have a verbose display with
git branch -v
Or
git branch -vv
To have a verbose display of all repos
git branch -vva

to change a branch name

```sh
git branch -m <old_name> <new_name>
```

## Git clone/branch/push (from remote / in local / to remote)

We start by cloning a remote repo.
N.B. we can equally start from a local repo, which we then push to a remote repo.
git clone [https]
We create and checkout a local branch “alpha”
git checkout -b alpha
After doing whatever necessary changes in the files of the alpha branch, we add
git add .
And then commit,
git commit -m “whatever message here”
Then, we can push to the remote repo.
The first push requires the -u flag along with the name of the new branch (in the remote repo),
git -u origin alpha
Git is smart enough to later know where to push. Later pushes requests only require
git push
N.B. Changes made in a specific branch are only seen in that branch and therefore the add, commit and push actions should be carried out in that branch. If we try to leave a branch without committing or stashing changes, we will receive an error.

## Git merge branch / push master / delete branch

Before merging the branch, we need to position ourselves in the master branch
git checkout master
Then, we merge the “alpha” branch to the master branch by typing
git merge alpha
N.B. In case we get conflict errors, they can be resolved in VSCode by checking the 2 versions and deciding what should be the final output file.
Once the merge is successful, we need to add, commit and push the master branch,
git add .
git commit -m “merged”
git push (for later pushes)
N.B. We can go to the “Insights” tab and then “network” to get a graph of the various pushes and merges.
After the merge, we can delete the local branch by typing
git branch -d alpha
To delete the branch remotely, we can use the github GUI “Code” ↦ “branches” or by code by pushing the name of the branch with a column,
git push origin :alpha

## Git checkout old commits

Before reverting, we need to check the log by typing
git log
We can display a more concise and comprehensible log by using the tags --graph and --oneline
git log --graph --oneline
N.B. We can also add the tags --all and --decorate
We can also check the graph by going to github.com and the network tab under insights in our repository.
Another git command to check reference log is
git reflog
If we want to copy a specific file, let’s say “index.html”, from an old repo, hash starts with “146fa”, we can do that by doing
git checkout 146fa -- index.html
We can checkout the whole repo by simply typing
git checkout 146fa
This will lead to a detached head. To return to the current head, we simply type
git checkout master
We can create a branch of the old commit in 2 ways
git checkout -b branch_name commit_sha
Or
git branch branch_name commit_sha
The first allows for the creation and direct checkout of the branch.

## Git reset commits

Git reset resets the repo to the version of the desired commit, removing all succeeding changes to that commit.
Of course, we first check the log to get the SHA (secure hash algorithm)
git log
We hard reset to an old commit
git reset --hard 45h2
Now the head is behind the remote repo. We can force push it.
git push --force
This will override the succeeding commits and put the head at the old commit.
Using force push is not generally recommended as it comes with the risk of losing newer commits. It is generally recommended to use
git push --force-with-lease

## Git revert commits

Git revert changes the revert made on files in a commit while keeping the other succind commits valid.
Of course, we first check the log to get the SHA (secure hash algorithm)
git log
We hard reset to an old commit
git revert 45h2
This will create a new commit point.
If the repo had a merge commit, then we should use
git revert -m 1 45h2
Using -m 1 tells git that this is a merge and we want to roll back to the parent commit on the master branch. You would use -m 2 to specify the develop branch.

## Git fetch

```bash
 git config --get remote.origin.fetch
```

## Git pull

## Git switch

## Get difference between old and new files

git diff
Or between two specific commits
git diff 7b06 e89a

Thanks for providing the link. Here's the revised text with the link added:

Here's the revised text with corrected English:
