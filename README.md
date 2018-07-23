# <p align="center"> Git Cheat Sheet
  <p align="center"> A personal cheat sheet that covers basic Git commands and information for reference.

## Helpful Resources/Related Links:
* [Codeacademy's Learn Git Course](https://www.codecademy.com/learn/learn-git)
* [ProGit eBook](https://git-scm.com/book/en/v2)
* [Atlassian's Tutorial on Git](https://www.atlassian.com/git/tutorials)
* [Interesting blog post that explains Git/Github in plain english](https://blog.red-badger.com/blog/2016/11/29/gitgithub-in-plain-english)
* [Interesting blog post on how to write a git commit message](https://chris.beams.io/posts/git-commit/)
* [Similar Git Cheatsheet](https://services.github.com/on-demand/downloads/github-git-cheat-sheet.pdf)
> This directory *C:\Program Files\Git\mingw64\share\doc\git-doc* holds interesting documentation of all the popular commands.

## <p align="center"> Basic Git Commands



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


### How to confirm that user.name & user.email keys either have values or are empty from configuration settings: 
* ` $ git config --list ` OR 
* ` $ git config -l `     OR
* ` $ git config user.name ` AND ` $ git config user.email `


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


### To inspect the contents of the working directory and staging area
` $ git status `


### To show the difference between the working directory and the staging area
` $ git diff `


### To show a log of all previous commits:
` $ git log `

```diff

- NOTE: 

In the output, notice:

A 40-character code, called a SHA, that uniquely identifies the commit. This appears in orange text.
The commit author (you!)
The date and time of the commit
The commit message

After running this command, if you're stuck on the page, you may need to press 'q' on your keyboard to restore the terminal.

```