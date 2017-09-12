# Das is GIT!
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
Now what left is to bind our **git project** with **git repository**. Execute below command within `git-workshop` repository. **Again, don't forget to change username in repository url!**

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

I have to admit `git log` doesn't display the information in the nicest way. My favorite tool for working with git log is [tig](https://jonas.github.io/tig/). I higly recomend to install it.

## Push
Going with the flow, the next step is to upload our first commit to cloud (origin). We can achive it with `git push` command. **Remember to change your user name**.

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

## Brunch
Think about **master** brunch as the root of the tree -finally everything all branches merge into master brunch.

The real deal working with version control tools is to create multiple brunches. The common scenario is to have a **master**, **develop**, **testing** brunch that will be deployed to equivalent environment. Lets create a **develop** brunch which will be rootede
