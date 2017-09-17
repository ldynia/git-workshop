# Das ist GIT!
Welcome to the workshop on how to use `git version control`. After finishing this tutorial you will be able to use `git` in your next project. Thought tutorial was written with the focus on bioinformaticians, it targets everyone who has no or limited knowledge of working with `git`.

## Requirements
Before starting this tutorial you have to fulfilled below requirements.

* [git](https://git-scm.com/) - installed
* [vim](https://vim.sourceforge.io/) - installed
* [python](https://www.python.org/) - installed
* [github](https://github.com/) or [gitlab](https://about.gitlab.com/) or [bitbucket](https://bitbucket.org/) - account
* access to a linux/unix terminal

## Assumption
I assume that a user has full field points spcified in requirements section.

## Problem definition
Have you ever found yourself in a situation that by mistake you deleted important to you files (such an assignment or latest fix to your source code code), or you had chance to collaborate on a document involving multiple contributors? If so and you didn't use a [version control](https://en.wikipedia.org/wiki/Version_control) tools then I have pity on you!  Those are one of many reasons why version control softwares were created in the first place. Version control or source control software allows you to keep track of changes introduced to file(s), recover deleted files, keep the log of changes, version your files and many more. `Git` is the most popular version control tool.

If the thing that I am writing now does not make sense, then don't worry. I will walk you through the various use-cases of using `git`.

## Conceptual model
A key to understand anything new is to develop conceptual model about the thing that you try to learn. A good conceptual model should be easily explainable to a kid. If you can do that then it means that you have big picture of the thing that you are talking about *und das is GIT! Ja?*

### Tree model
One way of looking at version control is to associate it with a tree. Every tree has many branches that originate in common root. Moreover, a branch as many leaves that with time appear along with the growth of a branch.

The essence of working with version control is basically to create branches and leaves. A branch symbolize development path or a direction of your work. A leave is a contribution to the branch it can be a line(s) of code, or a segment of text. It can be even a number of bytes introduce to image file.

### River model
If you don't dig the concept of a tree then I have second model that might come better to play. If you look at a river from an airplane perspective then, you will see a main riverbed where the river flows, and smaller riverbeds branching out of it. Along the riverbeds you will find a settlements. In this model the riverbeds symbolize directions or your work, and settlements stands for the contribution to your project.  

# Demo Project
In this tutorial I will walk you through basic things that you have to know about git and the frequent tasks which will become your bread and butter if it's about working with git. So lets started with our project.

## Git project

To create a **git project** we have to initialize a **.git** folder. The **.git** folder is noting more than a hidden directory that contains git's files. Git files track changes to all files within the git project.

```bash
# create git-workshop directory
ludd@E7450:~$ cd ~
ludd@E7450:~$ mkdir git-workshop
ludd@E7450:~$ cd git-workshop

# list all files (including hidden files) within git-workshop directory
ludd@E7450:~/git-workshop$ ls -la
total 8
drwxrwxr-x  2 user user 4096 Sep 11 16:34 .
drwxr-x--- 71 user user 4096 Sep 11 16:34 ..

# instantiate git repository
ludd@E7450:~/git-workshop$ git init
Initialized empty Git repository in /home/user/git-workshop/.git/

# again list all files within git-workshop directory
ludd@E7450:~/git-workshop$ ls -la
total 12
drwxrwxr-x  3 ludd ludd 4096 Sep 11 16:42 .
drwxr-x--- 71 ludd ludd 4096 Sep 11 16:34 ..
drwxrwxr-x  7 ludd ludd 4096 Sep 11 16:42 .git
```
If you encounter a `.git` directory within a folder then, it means that this folder is a git project.

## Git repository
A **git repository** is nothing more than your git project stored in a cloud. The most used cloud for git repositories is [github.com](https://github.com/) so lets work with it - you are free to work with any source code management service.

To create a **github repository** do as follow

1. Go to [github.com](https://github.com/)
2. Sign in
3. Clink button called **new repository**
4. Enter project name called **git-workshop**
5. Click button called *Create repository*
6. Click button called *Https* and copy repository's url. Remember to change user name to your's github username!!!! eg. `https://github.com/ldynia/git-workshop.git`

Voila, we created our first git repository!

## Git project + Git repository
Now what left is to bind our **git project** with **git repository**. Execute below command within `git-workshop` repository. **Don't forget to change username in repository url!**

```bash
ludd@E7450:~/git-workshop$ git remote -v
ludd@E7450:~/git-workshop$ git remote add origin https://github.com/ldynia/git-workshop.git
ludd@E7450:~/git-workshop$ git remote -v
origin	https://github.com/ldynia/git-workshop.git (fetch)
origin	https://github.com/ldynia/git-workshop.git (push)
```

## Vocabulary
To makes things easier lets level up and gain necessary vocabulary to work with git.
* **origin** - refers to git repository hosted in the cloud.
* **branch** - direction of your work within your git project.
* **master** - default branch for any git project.
* **commit** - amount of information to be contributed to a branch.
* **push** - action of sending commits to origin (cloud).
* **pull** - action of retrieving commits from origin (cloud).
* **HEAD** - latest commit on active branch.

## Commit
If we thing about process of developing a program (writing a source code) then it's nothing more than adding/removing/updating/renaming a files and directories. Saying that lets contribute first file to our project and create our first commit. You will gonna do this step million of times then please put attention into it.


```bash
# create empty file and check status of current work
ludd@E7450:~/git-workshop$ echo "My first commit" > readme.md
ludd@E7450:~/git-workshop$ git status
On branch master
Initial commit
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	readme.md
nothing added to commit but untracked files present (use "git add" to track)

# add untracked file and check status
ludd@E7450:~/git-workshop$ git add readme.md
ludd@E7450:~/git-workshop$ git status
On branch master
Initial commit
Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   readme.md

# create first commit
ludd@E7450:~/git-workshop$ git commit -m'init -adding readme.md'
[master (root-commit) aec47ab] init -adding readme.md
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 readme.md
```

## Log
At any time you can see the log of your git project. To do so execute `git log` command. The log is displayed top down -top being the latest commit.

```bash
# display log
ludd@E7450:~/git-workshop$ git log
commit aec47abf6280371fe7c26f601ef18eae01a5e74b
Author: ldynia <ludd@cbs.dtu.dk>
Date:   Tue Sep 12 11:15:56 2017 +0200

    init -adding readme.md
```

As you can see log contains of four elements.
* **hash** - unique identifier of commit.
* **author** - person who contributed changes.
* **date** - time of contribution.
* **message** - message associated with commit.

I have to admit that `git log` doesn't display the information in the nicest way. My favorite tool for working with git log is [tig](https://jonas.github.io/tig/). I higly recomend to install it.

## Push
Going with the flow, the next step is to upload our first commit to cloud (origin). We can achive it with `git push` command. **Remember to change your user name!!!**.

```bash
ludd@E7450:~/git-workshop$ git push origin master
Username for 'https://github.com': ldynia
Password for 'https://ldynia@github.com':
Counting objects: 3, done.
Writing objects: 100% (3/3), 213 bytes | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/ldynia/git-workshop.git
 * [new branch]      master -> master
```

Now if you will visit your github repository you will see your first commit stored at the remote origin. **Remember to change your user name**. [https://github.com/ldynia/git-workshop](https://github.com/ldynia/git-workshop)

## Branch
Think about **master** branch as the root of the tree -finally everything all branches merge into master branch.

The real deal working with version control tools is to create multiple branches. The common scenario is to have a **master**, **develop**, **testing** branch that will be deployed to equivalent environment. Lets create a **develop** branch which will is roots from **master** branch.

```bash
# create new branch
ludd@E7450:~/Coding/workshops/git-workshop$ git checkout -b develop
Switched to a new branch 'develop'

# display all available branches
ludd@E7450:~/git-workshop$ git branch
* develop
  master
```

The **\*** (asterisk) next to branch name indicates that **develop** brunch is your active brunch. Other words we are working on **develop** branch now.

Lets commit new file to the **develop** branch and checkout to the master branch and investigate content of our directory.
```bash
# create commit on develop branch
ludd@E7450:~/git-workshop$ touch dev_file
ludd@E7450:~/git-workshop$ git add dev_file
ludd@E7450:~/git-workshop$ git commit -m'adding dev file'
[develop 1a627dc] adding dev file
1 file changed, 0 insertions(+), 0 deletions(-)
create mode 100644 dev_file

# list content of directory
ludd@E7450:~/git-workshop$ ls
dev_file readme.md

# checkout to master branch and list content of directory
ludd@E7450:~/git-workshop$ git checkout master
Switched to branch 'master'
ludd@E7450:~/git-workshop$ ls
readme.md
```
What the hell append ? are we missing a file along with the 18 minutes of Watergate? Didn't we create a file few seconds ago? Yes we did. Hold your forces and don't panic the file is still there. What happend is we created a file on the develop branch and it is still there. Lets have a loop at it.

```bash
ludd@E7450:~/git-workshop$ git checkout develop
Switched to branch 'develop'

# files are still here
ludd@E7450:~/git-workshop$ ls
dev_file  readme.md
```

Now lets see the history of our work using `git log` command.

```bash
# list history of commits
ludd@E7450:~/git-workshop$ git log --oneline
1a627dc adding dev file
aec47ab init -adding readme.md
```

Things look ok aren't they? Lets see the commits on the master branch.

```bash
ludd@E7450:~/git-workshop$ git checkout master
Switched to branch 'master'
ludd@E7450:~/git-workshop$ git log --oneline
aec47ab init -adding readme.md
```
Can you see that we are behind with one commit on the master branch? This commit contains our file, we will be able to include it into master branch wit `git merge` commad.

## Merge
Another thing that you will be frequntly doing with git is to merge a commits between the branches -I'm telling you that you will be bored with it.  To merge changes from one branch to another you have to switch to the branch that you want to merge into and execute `git merge <branch_tom_merge_with>` command.

```bash
ludd@E7450:~/git-workshop$ git checkout master
Already on 'master'
ludd@E7450:~/git-workshop$ git merge develop
Updating aec47ab..1a627dc
Fast-forward
 dev_file | 0
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 dev_file
ludd@E7450:~/git-workshop$ git log --oneline
 1a627dc adding dev file
 aec47ab init -adding readme.md
ludd@E7450:~/git-workshop$ ls
dev_file  readme.md
```

## Merge conflicts
So far so good. However, things not always go as expected. Often you will find yourself in situation of resolving a **marege conflicts**. A merge conflict in context of version control is a situation that happens when you try to merge a files that has overlapping and conflicting information on those branches. Here is an example.

```bash
# create conflicting line file on master
ludd@E7450:~/git-workshop$ echo "roses are blue" > c.txt
ludd@E7450:~/git-workshop$ git add .
ludd@E7450:~/git-workshop$ git commit -m'blue'

# create conflicting line file on develop
ludd@E7450:~/git-workshop$ git checkout develop
ludd@E7450:~/git-workshop$ echo "roses are red" > c.txt
ludd@E7450:~/git-workshop$ git commit -m'red'

# merge branches
ludd@E7450:~/git-workshop$ git checkout master
ludd@E7450:~/git-workshop$ git merge develop
Auto-merging c.txt
CONFLICT (add/add): Merge conflict in c.txt
Automatic merge failed; fix conflicts and then commit the result.

# investigate branch
ludd@E7450:~/git-workshop$ git status
On branch master
You have unmerged paths.
  (fix conflicts and run "git commit")
Unmerged paths:
  (use "git add <file>..." to mark resolution)
	both added:      c.txt
no changes added to commit (use "git add" and/or "git commit -a")
```

## Looking into merge conflict
Don't think about merge conflict as something bad happed. Actually, merge conflicts save yours ass! To resolve merge conflict we will have to investigate where it occured file. Lets look into the file that contains merge conflict.

```bash
ludd@E7450:~/git-workshop$ cat c.txt
<<<<<<< HEAD
roses are blue
=======
roses are red
>>>>>>> develop
```

Important thing to notice.
* **<<<<<<<** - this symbol indicates where conflicting line starts.
* **>>>>>>>** - this symbol indicates where conflicting line ends.
* **\=\=\=\=\=\=\=** - this symbol indicates division between conflicting lines.

The important thing to know is the **HEAD** and order in which the conflict is structured. Upper part that contains the **HEAD** text, refers to our current active brunch - in our case it is the master branch. Lower part refers to branch that we are merging with - this time it is develop branch.

## Fixing merge conflicts
Fixing merge conflict is nothing more than figuring out which line(s) are wrong and removing them. I will use **vim**, to do it - you are welcome to use any text editor of your choice.

```bash
# edit, save and display content of conflicting file
ludd@E7450:~/git-workshop$ vim c.txt
ludd@E7450:~/git-workshop$ cat c.txt
roses are red

# commit changes
ludd@E7450:~/git-workshop$ git add c.txt
ludd@E7450:~/git-workshop$ git commit -m'resolving merge conflict'
[master af8238a] resolving merge conflict

# check the log
ludd@E7450:~/git-workshop$ git log --oneline
af8238a resolving merge conflict
e2bd427 red
402e2c5 adding c file
1a627dc adding dev file
aec47ab init -adding readme.md
```

Tap yourself in the shoulder and shout Wunderbar!, because we just resolved our first merge conflict.

## Amend
Sometimes you will find yourself in the situation where you forgot to add something important to the last commit, and the thing is not worth it to create new commit. This is where `git commit --amend` comes with help.

```bash
# amend text
ludd@E7450:~/git-workshop$ echo "sky is blue" >> c.txt
ludd@E7450:~/git-workshop$ git add c.txt
ludd@E7450:~/git-workshop$ git commit --amend
```

## Stash
Writing a software is a task that requires a focus. You have to go into the focus zone and start translating a conceptual models (requirements) into tangible things understandable by a computer. More likely, during process of writing code you will be interrupted, and request to fix some bug that appeared in previous commit(s). `git stash` is the tool that solves exactly this problem. It does what it says. It stashes uncommitted changes, and place you at the **HEAD**. Lets put our hands on it.


```bash
# we start working on some new feature
ludd@E7450:~/git-workshop$ echo "I am in the zone" >> c.txt
ludd@E7450:~/git-workshop$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   c.txt

no changes added to commit (use "git add" and/or "git commit -a")

# your colleague comes and ask you to fix a bug
ludd@E7450:~/git-workshop$ git stash
Saved working directory and index state WIP on master: 2289968 resolving merge conflict
HEAD is now at 2289968 resolving merge conflict

# check if something is stashed
ludd@E7450:~/git-workshop$ git stash list
stash@{0}: WIP on master: 2289968 resolving merge conflict

# check that there is nothing to commit
ludd@E7450:~/git-workshop$ git status
On branch master
nothing to commit, working directory clean

# now you do the fix and create commit;
ludd@E7450:~/git-workshop$ doing stuff ...

# once you fixed the bug you can comeback to what you started
ludd@E7450:~/git-workshop$ git stash apply
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   c.txt

no changes added to commit (use "git add" and/or "git commit -a")

# check that we are back on track
ludd@E7450:~/git-workshop$ cat c.txt
roses are red
sky is blue
I am in the zone
```
