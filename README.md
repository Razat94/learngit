# <p align="center"> Git Cheat Sheet </p>
  <p align="center"> A personal cheat sheet that covers basic Git commands and information for reference. </p>
  <p align="center"> 
  The following is a compilation of all the useful commands/resources I've found while learning Git. 
  By no means did I write any of this.
  </p>


## Resources/Related Links:
* [Codeacademy's Learn Git Course](https://www.codecademy.com/learn/learn-git)
* [ProGit eBook](https://git-scm.com/book/en/v2)
* [Atlassian's Tutorial on Git](https://www.atlassian.com/git/tutorials)
* [Interesting blog post that explains Git/Github in plain english](https://blog.red-badger.com/blog/2016/11/29/gitgithub-in-plain-english)
* [Interesting blog post on how to write a git commit message](https://chris.beams.io/posts/git-commit/)
* [Similar Git Cheatsheet](https://services.github.com/on-demand/downloads/github-git-cheat-sheet.pdf)
* [Another Git Cheatsheet](https://orga.cat/posts/most-useful-git-commands)
> The directory *C:\Program Files\Git\mingw64\share\doc\git-doc* holds interesting documentation for all of the popular commands.


## <p id = "toc"> Table of Contents </p>
1. [Configuration](#config)
2. [Basic Git commands](#basicGit)
3. [Undoing Changes](#undo)


<br></br>
## <p align="center" id = "config"> Configuration | [Back to ToC](#toc) </p>


### How to display help information about Git
` $ git help `


### How to sign in/set Github Account in Git Bash console:
```
$ git config --global user.name "John Doe"
$ git config --global user.email "johndoe@example.com" 
```


### How to sign out/unset Github Account in Git Bash console:
```
$ git config --global --unset user.name
$ git config --global --unset user.email
```

The top answer of [this stackoverflow question](https://stackoverflow.com/questions/38549834/how-to-sign-out-in-git-bash-console-in-windows/38553149#38553149)
states that in order to properly sign out and be asked again for username/password when commiting to a project, this needs to be done:

> Go to: Control Panel -> User Accounts -> Manage your credentials -> Windows Credentials -> Generic Credentials
> <br> There, you fill find some credentials related to Github. Click on them and then click "Remove". 

I found that this method simply deletes a personal access token from your github account. 
In doing so, yes, it is impossible to push a commit without signing into an account first.

<strong> However </strong> I noticed that this method fails in a certain regard.
Suppose I want to push a commit from an account that is different from the account's default identity. Using the above method will not work because 
[commits in Git is associated with the user.email key.](https://help.github.com/articles/setting-your-commit-email-address-in-git/)
In doing so, I would've made a commit from an account that is associated with the value of the <em>user.email</em> key, 
and not from the account that I typed into this alert window:

<div align = "center"> <img src = "images/login.PNG"> </div>

Better yet, if I unset the <em>user.name</em> and <em>user.email</em> keys, I recieve this message when I attempt to make a commit:
```
*** Please tell me who you are.

Run

  git config --global user.email "you@example.com"
  git config --global user.name "Your Name"

to set your account's default identity.
Omit --global to set the identity only in this repository.

fatal: unable to auto-detect email address (got 'Razat@DESKTOP-UK2NEC1.(none)')
```


### How to confirm that user.name & user.email keys either have values or are empty from configuration settings: 
* ` $ git config --list ` OR 
* ` $ git config -l `     OR
* ` $ git config user.name ` AND ` $ git config user.email `


<br></br>
## <p align="center" id = "basicGit"> Basic Git Commands | [Back to ToC](#toc) </p>


<img src = "images/learngit.PNG">

A Git project can be thought of as having three parts:

> 1. A Working Directory: where you'll be doing all the work: creating, editing, deleting and organizing files
> 2. A Staging Area: where you'll list changes you make to the working directory
> 3. A Repository: where Git permanently stores those changes as different versions of the project

The Git workflow consists of:
> * editing files in the working directory
> * adding files to the staging area
> * saving/commiting changes to a Git repository. 

Git essentially has 4 main states for the files in your local repo: 
[Source](https://stackoverflow.com/questions/7564841/concept-of-git-tracking-and-git-staging/15803429)

<img src = "images/lifecycle.png" href = "https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository" >

* <strong> untracked: 	</strong> Untracked files are files that Git knows nothing about it. 
				In most cases, thess files are typically new, or have been removed.
				If I have a new file, and I run ` $ git add <file> `, it  becomes:

* <strong> staged:	</strong> The file is now in the staging area. 
				Git now knows that the file exists, and the files are now being tracked. 
				It is now part of the next commit batch (called the <em>index</em>). 
				If you git commit, it becomes:

* <strong> unmodified/unchanged:</strong> The file has not changed since its last commit. If you modify it, it becomes:

* <strong> modified/unstaged:  	</strong> The file has been modified but is not part of the next commit yet. 
					  You can stage it again with ` $ git add ` command.


Also: You can untrack an uncommited file with git rm --cached filename and unstage a staged file with git reset HEAD <file>


It is important to note that Staged files are files that are listed in the Staging Area. 
Unstaged files are files that aren't staged yet i.e. files that are in working directory but not in the staging area.
It is also important to note that Tracked/Untracked files is synonymous to Staged/Unstaged files.

> In Git, the commit you are currently on is known as the HEAD commit. 
> In many cases, the last, most recently made commit is the HEAD commit.


### How to (re)initialize an empty Git repository:
` $ git init `

```diff
- NOTE: This command creates a hidden folder named `.git` in your working directory.
```


### How to completely delete a git repository:
` $ rm -rf .git `

```diff
- NOTE: As an alternative, you can just manually delete the folder `.git` from the file directory.
```


### How to adds all of the files from the working directory to the staging area
` $ git add . `


### How to inspect the contents of the working directory and staging area
` $ git status `


### How to show the difference between the working directory and the staging area
` $ git diff `


### How to permanently store the file changes from the staging area in the repository
` $ git commit -m "message" `


### …or push an existing Git repository from the command line to a Github repo
> Run this command initially if you're pushing to a new Github repo:
> <br> ` $ git remote add origin [Github Repo URL].git `

` $ git push -u origin master `

Run the command 
` $ git push -f origin master ` 
to force a push to a repo that contains work that you <strong> don't </strong> have locally.
Using this command will fix this error:

```diff
To git@github.com:roseperrone/project.git
 ! [rejected]        master -> master (fetch first)
error: failed to push some refs to 'git@github.com:roseperrone/project.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first merge the remote changes (e.g.,
hint: 'git pull') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

[Source](https://stackoverflow.com/questions/17291995/push-existing-project-into-github#18329034)

### How to show a log of all previous commits:
` $ git log `

```diff
- NOTE: 
In the output, notice:

* A 40-character code, called a SHA, that uniquely identifies the commit.
> From now on, whenever I say 'SHA', I will refer to the first 7 digits of this number.
* The commit author
* The date and time of the commit
* The commit message
```

> To show a log of each previous commit printed on individual lines, use:
> ` $ git log --oneline ` OR if you want to see the full SHA number, use: 
> ` $ git log --pretty=oneline `

> To show the log of the last two commits:
> ` $ git log -2 `

> To only display commits of a particular file:
> ` $ git log [file] `

> When you run this command, you will need to press the "Enter" key to see one previous commit, or the "Space" key to see a bunch of previous commits. 

> After running this command, if you're stuck on the page, you may need to press 'q' on your keyboard to restore the terminal.


### Show list of modifiled files, how many files were changed, and how many lines in those files were added and removed in last two commits: 
` $ git log -2 --stat `


### To only lines that have been modified between last two commits:
` $ git log -2 -U0 `


### How to show commit details by SHA
` $ git show SHA `
> To see some abbreviated stats for each commit: ` $ git show SHA --stat ` 

> To see the HEAD commit, enter: git show HEAD


### How to show the content of a particular file from a specific commit:
` $ git show SHA:[filename.fileextension] `
[Source](https://stackoverflow.com/questions/424071/how-to-list-all-the-files-in-a-commit)


### To see a list of modified files, how many files were changed, and how many lines in those files were added and removed. 
` $ git diff SHA1 SHA2 --stat `


### How to show only lines that have been modified between two commits:
` $ git diff -U0 SHA1 SHA2 `
[Source](https://stackoverflow.com/questions/18810623/git-diff-to-show-only-lines-that-have-been-modified)
> This also works: ` $ git diff --unified=0 SHA1 SHA2 `


### How to show only the file names that changed between two commits:
` $ git diff --name-only SHA1 SHA2 `
[Source](https://stackoverflow.com/questions/1552340/how-to-list-only-the-file-names-that-changed-between-two-commits)
> This works too: ` $ git show --name-status SHA1 ` 


### How to see list of all files in a commit:
` $ git diff-tree --no-commit-id --name-only -r SHA `


### How to see a list of files under git version control
` $ git ls-files `


### To remove a file in Git:
` $ git rm [file] ` 
> Remember: use this command to remove files from both the staging area and the working directory.

> In order to remove a file with this command, it must first be under git version control. 
> Files that have not been added yet (Untracked files) or are ignored (using .gitignore or .git/info/exclude files) will nnot be added.


### To rename a file in Git:
` $ git mv [file_from] [file_to] ` 


### How to list total commits by author (sorted by commit count):
` $ git shortlog -sn `


### How to list remote branches that have been tracked locally: [Source](https://stackoverflow.com/questions/3471827/how-do-i-list-all-remote-branches-in-git-1-7)
` $ git branch -r `


<br></br>
## <p align="center" id = "undo"> Undoing Changes | [Back to ToC](#toc) </p>


### Viewing an old commit | [Source](https://www.atlassian.com/git/tutorials/undoing-changes)
Let’s say your project history looks something like the following:

```diff
$ git log --oneline

b7119f2 Continue doing crazy things
872fa7e Try something crazy
a1e8fb5 Make some important changes to hello.txt
435b61d Create hello.txt
9773e52 Initial import
```

You can use <em>git checkout</em> to view the "Make some import changes to hello.txt" commit as follows:
` $ git checkout a1e8fb5 `

This makes your working directory match the exact state of the <strong>a1e8fb5</strong> commit. 
You can look at files, compile the project, run tests, and even edit files without worrying about losing the current state of the project. 
Nothing you do in here will be saved in your repository. 
To continue developing, you need to get back to the "current" state of your project:
` $ git checkout master `


### How to reset the file in the WORKING DIRECTORY to the HEAD commit:
` $ git checkout HEAD filename `


### How to reset the file in the STAGING AREA to be the same as the HEAD commit.
` $ git reset HEAD filename `


### How to resets HEAD to a previous commit in your commit history:
` git reset SHA `


### How to amend (make additional changes) to the most recent commit: 
` $ git commit --amend `

As an example, 
if you commit and then realize you forgot to stage the changes in a file you wanted to add to this commit, 
you can do something like this:

```diff
$ git commit -m 'initial commit'
$ git add forgotten_file
$ git commit --amend
```

By doing this, you will only end up with one commit, where the new changes will be amended to the previous commit.

> To just change the message of the last commit: 
> ` $ git commit --amend -m "New commit message" `