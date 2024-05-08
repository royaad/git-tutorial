# Git

In this document, we delve into various Git commands and their functionalities. You'll notice that commands performing the same actions are presented alongside each other, with one version highlighted as a comment to emphasize its shorter form.

Let's explore the world of Git commands together!

## Git Default Branch (GUI)

To establish the default branch name through the git GUI, navigate to Settings → Repositories. Subsequently, input the desired default branch name for your new personal repositories.

Here's the rephrased text in Markdown format:

## `git` Basics

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
# git --help config
# git help config
```

Additionally, to open a help page in the web browser for terminal assistance, you can use:

```bash
git config -h
```

## Get difference between old and new files

git diff
Or between two specific commits
git diff 7b06 e89a

Thanks for providing the link. Here's the revised text with the link added:

Here's the revised text with corrected English:

## `git` Configuration

`git config` is used to configure various aspects of Git. It has three levels:

- Global: Configuration settings that apply globally to the user's system.
- System: Configuration settings that apply to every user on the system and all repositories.
- Local: Configuration settings that apply only to the current repository.

### Getting Configuration Information

- To obtain a list of git configurations:

  ```bash
  git config -l
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
  # git config --get user.name
  ```

### Configuring Git

It is usually a good practice to configure the global configs of git as it offers ease of use for later.

- Configure username globally:

  ```bash
  git config --global user.name "royaad"
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

## Config CRLF

Windows, Linux, and Mac use different control characters to mark a line break in a text file. Windows uses two characters CR LF; Unix (and macOS starting with Mac OS X 10.0) only uses LF; and the classic Mac OS (before 10.0) used CR. By default, git is set to auto-correct the CRLF differences. We can check this by typing

```bash
git config --system -l
```

, and we'll see the option `core.autocrlf=true`. This will lead to a warning message: `warning: LF will be replaced by CRLF`. To suppress these messages, we can set `autocrlf` to false by typing:

```bash
git config --global core.autocrlf false
```

For further readings, refer to [link 1](https://stackoverflow.com/questions/1552749/difference-between-cr-lf-lf-and-cr-line-break-types) and [link 2](https://stackoverflow.com/questions/17628305/windows-git-warning-lf-will-be-replaced-by-crlf-is-that-warning-tail-backwar).

## Git add a remote repo

Add a remote repo
git remote add origin [https link]
Check value of remote repo
git remote -v

## Git add/remove or stage unstage files

Add/stage a specific file (e.g. index.html)
git add index.html
Add/stage all files
git add . or git add \*
Remove/unstage a specific file (e.g. index.html)
git reset head index.html or git restore --staged index.html

## Git Push

When we push a repo, we must specify the origin (remote repo) and the branch. The most basic syntax is:
git push [remote name] [branch]
Or more specifically,
git push origin master
Since the remote repo was given the name origin when we added it. It should be noted that we can add many remote repos in the same local git repo.
When we are pushing for the first time, if the branch doesn’t exist we must set it up, and thus we must type:
git push --set-upstream origin master
Or equally
git push -u origin master
If we are pushing towards another branch named “alpha”, then the command becomes
git push -u origin alpha

## SSH (Secure Shell)

Check SSH
ssh
Create an SSH key, encryption type rsa and 4096 bits
ssh-keygen -t rsa -b 4096 -C "royaad@live.com"
Bind to github (execute from the local git repo)
ssh -T git@github.com

## Git init/push local repo (towards an empty remote repo)

Open command prompt in the folder to push
Initialize the folder as a local repository
git init
Stage the files for their first commit
git add .
To check the status
git status
Commit the files
git commit -m "first commit"
Add the url of the repository (Only the fist time)
git remote add origin [https]
Push repository
git push -u origin master (the -u flag is used only the first time)
Enter username and password (Only the first time)

## Git init/push local repo (towards a non-empty remote repo)

Open command prompt in the folder to push
Initialize the folder as a local repository
git init
Stage the files for their first commit
git add .
To check the status
git status
Commit the files
git commit -m "first commit"
We can add all changed files and commit using (skip git add for modified files only)
git commit -am "first commit"
Add the url of the repository (Only the first time)
git remote add origin [https]
Since the remote repo is not empty, we should first pull the remote files. However, this is not a normal pull since the two repos do not have a related history. One must be careful that the pull will not cause a loss of files. To pull the repo:
git pull --allow-unrelated-histories origin
Push repository (the master branch is already set. No need for the -u flag.
git push origin master
Enter username and password (Only the first time)

## Git commit --amend

In case we do a commit then we realize we want to change it we can use
git commit --amend
For example, we can stage the files
git add .
Then amend then to the last commit
git commit --amend -m “new commit message”

## Cloning a remote repo

Open command prompt in the directory where you wish to clone the repo folder
Clone the folder in the local repository
git clone [https]
Stage the files for their first commit
git add .
Commit the files
git commit -m "first commit"
The cloned repo is already connected to the remote repo and so we can directly push
git push origin master

## Git Branching

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
