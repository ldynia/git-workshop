# Das ist GIT!
Welcome to the workshop on how to use `git version control`. After finishing this tutorial you will be able to use [Git](https://git-scm.com/doc) in your next project. Thought tutorial was written with the focus on bioinformaticians, it targets everyone who has no or limited knowledge of working with Git.

## Requirements
Before starting this tutorial you have to fulfilled below requirements.

* [git](https://git-scm.com/) - installed
* [vim](https://vim.sourceforge.io/) - installed
* [github](https://github.com/) or [gitlab](https://about.gitlab.com/) or [bitbucket](https://bitbucket.org/) - account
* access to a linux/unix terminal

## Assumption
I assume that a user has full field points specified in requirements section.

## History
Let me ask you this question. Try to name a software that has the grates impact on humanity? It is difficult one, but in my opinion it is [Linux](https://en.wikipedia.org/wiki/Linux) initially written by [Linus Torvalds](https://en.wikipedia.org/wiki/Linus_Torvalds).

Without Linux you would have to throw out all smartphones, tablets and tvs that run on Android and iOS. Content of the web would shrink at least 60%. We would not send a humans into the space. And many many more.

But how you write a software that counts 15+ million lines of code? For suer it can't be written by a single man. Further more in project like this you would like to keep track who added changes (when and what), files being removed, retrieve deleted files, resolve overlaps of conflicting information, version the code, fix bugs, fix security volubilities etc.

Another brilliant thing that Linus Torvalds wrote for the purpose of facilitating development of the Linux kernel was [Git](https://en.wikipedia.org/wiki/Git). Today git is the most popular version control/source control software used by developers. So, if you didn't use a [version control](https://en.wikipedia.org/wiki/Version_control) tools then I have pity on you!

If the thing that I am writing now does not make sense to you then don't worry. I will walk you through the various use-cases of using Git.

## Inner Workings
Git thinks of data as a set of snapshots. Every time you create a commit, or save the state of your project, Git takes a picture of all your files and stores a reference to that snapshot. If files have not changed then Git doesn’t store the file again, installed it links to the previous identical file it has already stored.

Because of that you can contribute changes to your project off-line and next time when you are on-line you will sync the difference between your local version of repository with the one online.

Everytime you create a commit Git creates hash (SHA-1 checksum), this way it's impossible to change content of a file without Git knowing about it.

## Conceptual model
A key to understand anything new is to develop conceptual model about the thing that you try to learn. A good conceptual model should be easily explainable to a kid. If you can do that then it means that you have a big picture of the thing that you are talking about, *und das is GIT! Ja?*

### Tree
One way of looking at version control is to associate it with a tree. Every tree has many branches that originate in common root. Moreover, a branch as many leaves that with time appear along with the growth of a branch.

The essence of working with version control is basically to create branches and leaves. A branch symbolize development path or a direction of your work. A leave is a contribution to the branch it can be a line(s) of code, or a segment of text. It can be even a number of bytes introduce to image file.

# Demo Project
In this tutorial I will walk you through basic things that you have to know about git and the frequent tasks which will become your bread and butter if it's about working with git. So lets started with our project.

## Git config
Before we start working with git we have to configure it. Lets add basic information associated with our git user such  **username** and **email**. **Remember to set appropriate username and email to yours account!**  

```shell
$ git config --global user.email "jon"
$ git config --global user.username "jon@do.it"
```  

## Git local repository
**Git repository** is a **.git** folder located in yours project directory. The **.git** folder is a hidden directory that contains git's files -Git files track changes to all files within your project.

Lets create our first project and within the project we will create git repository. We will refer to this repository as a **local repository** -because it will resides locally on our machine.

```shell
# create git-workshop directory
$ cd ~
$ mkdir git-workshop
$ cd git-workshop

# list all files (including hidden files) within git-workshop directory
$ ls -la
total 8
drwxrwxr-x  2 user user 4096 Sep 11 16:34 .
drwxr-x--- 71 user user 4096 Sep 11 16:34 ..

# instantiate git repository
$ git init
Initialized empty Git repository in /home/user/git-workshop/.git/

# again list all files within git-workshop directory
$ ls -la
total 12
drwxrwxr-x  3 ludd ludd 4096 Sep 11 16:42 .
drwxr-x--- 71 ludd ludd 4096 Sep 11 16:34 ..
drwxrwxr-x  7 ludd ludd 4096 Sep 11 16:42 .git
```

If you encounter a `.git` directory within a folder then, it means that this folder is a git repository.

## Git remote repository
**Remote Git repository** is nothing more than your local Git repository uploaded to cloud -in short it is called **remote**.  The most used cloud for git repositories is [github.com](https://github.com/), and we will work with it- you are free to work with any source code management service (cloud).

To create a **github repository** do as follow

1. Go to [github.com](https://github.com/)
2. Sign in
3. Clink button called **new repository**
4. Enter project name called **git-workshop**
5. Click button called *Create repository*
6. Click button called *Https* and copy repository's url. Remember to change user name to your's github username!!!! eg. `https://github.com/ldynia/git-workshop.git`

Voila, we created our first git repository!

## Binding local with remote
Now what left is to bind offline (**local**) repository with online (**remote**). Execute below command within `git-workshop` directory. **Don't forget to change username in repository url!**

```shell
$ git remote -v
$ git remote add origin https://github.com/ldynia/git-workshop.git
$ git remote -v
origin	https://github.com/ldynia/git-workshop.git (fetch)
origin	https://github.com/ldynia/git-workshop.git (push)
```

## Vocabulary
To makes things easier lets level up and gain necessary vocabulary to work with git.
* **remote** - refers to git repository hosted in the cloud.
* **origin** - refers to branch on remote.
* **branch** - direction of your work within your git repository.
* **master** - default branch for any git repository.
* **commit** - amount of information to be contributed to a branch.
* **push** - action of sending commits to origin (cloud).
* **pull** - action of retrieving commits from origin (cloud).
* **HEAD** - latest commit on active branch.

## Commit
If we thing about process of developing a program (writing a code) then it's nothing more than adding/removing/updating/renaming a files and directories.

Saying that lets contribute first file to our project and create our first commit. You gonna do this step million times!


```shell
# create empty file and check status of current work
$ echo "My first commit" > readme.md
$ git status
On branch master
Initial commit
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	readme.md
nothing added to commit but untracked files present (use "git add" to track)

# add untracked file and check status
$ git add readme.md
$ git status
On branch master
Initial commit
Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   readme.md

# create first commit
$ git commit -m'init -readme.md'
[master (root-commit) aec47ab] init -adding readme.md
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 readme.md
```

## Log
At any time you can see the log of your git repository. To do so execute `git log` command. The log is displayed top down -top being the latest commit.

```shell
# display log
$ git log
commit 166e35068dd1642ef21a72ce77ea4056f73c45a0
Author: ldynia <ludd@cbs.dtu.dk>
Date:   Tue Sep 12 11:15:56 2017 +0200

    init -readme.md
```

As you can see log contains of four elements.
* **hash** - unique identifier of commit (SHA-1).
* **author** - person who contributed changes.
* **date** - time of contribution.
* **message** - message associated with commit.

I have to admit that `git log` doesn't display the information in the nicest way. My favorite tool for working with git log is [tig](https://jonas.github.io/tig/). I higly recomend to install it.

## Push
Going with the flow, the next step is to upload our first commit to cloud (remote). We can achieve it with `git push` command. **Remember to change your user name!!!**.

```shell
$ git push origin master
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
Think about **master** branch as the root of the tree -eventually all branches merge into master branch.

The real deal working with version control tools is to create multiple branches. The common scenario is to have a **master**, **develop**, **testing** branch that will be deployed to equivalent environment. Lets create a **develop** branch which roots from **master** branch.

```shell
# create new branch
/Coding/workshops/git-workshop$ git checkout -b develop
Switched to a new branch 'develop'

# display all available branches
$ git branch
* develop
  master
```

The **\*** (asterisk) next to branch name indicates that **develop** brunch is your active brunch. Other words we are working on **develop** branch now.

Lets commit new file to the **develop** branch and checkout to the master branch and investigate content of our directory.
```shell
# create commit on develop branch
$ touch d.txt
$ git add d.txt
$ git commit -m'd.txt'
[develop 1a627dc] adding dev file
1 file changed, 0 insertions(+), 0 deletions(-)
create mode 100644 d.txt

# list content of directory
$ ls
d.txt readme.md

# checkout to master branch and list content of directory
$ git checkout master
Switched to branch 'master'
$ ls
readme.md
```
What the hell append? are we missing a file along with the 18 minutes of Watergate? Didn't we create a file few seconds ago? Yes we did. Hold your forces and don't panic the file is still there. What happened is, we created a file (commit) on the develop branch and we switch the branches. Becaouse of that master branch is behind the develop branch, and because of that we cannot see the file on master branch. To much talking. Lets have a loop at it.

```shell
$ git checkout develop
Switched to branch 'develop'

# files are still here
$ ls
d.txt  readme.md
```

Now lets see the history of our work using `git log` command.

```shell
# list history of commits
$ git log --oneline
d296a37 d.txt
166e350 init -readme.md
```

Things look ok aren't they? Lets see the commits on the master branch.

```shell
$ git checkout master
Switched to branch 'master'

$ git log --oneline
166e350 init -readme.md
```
Can you see that now we are behind with one commit on the master branch? This commit contains our file, we will be able to include it into master branch wit `git merge` commad.

## Merge
Another thing that you will be frequntly doing with git is to merge a commits between the branches -I'm telling you that you will be bored with it. To merge changes from one branch to another you have to switch to the branch that you want to merge into and execute `git merge <branch_tom_merge_with>` command.

```shell
$ git checkout master
Already on 'master'

$ git merge develop
Updating 166e350..d296a37
Fast-forward
 d.txt | 0
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 d.txt

$ git log --oneline
 1a627dc adding dev file
 aec47ab init -adding readme.md

$ ls
d.txt  readme.md
```

## Merge conflicts
So far so good. However, things not always go as expected. Often you will find yourself in situation of resolving a **marege conflicts**. A conflict in context of version control is a situation when you try to merge a files that has overlapping and conflicting information on branches that you are trying to merge. Here is an example.

```shell
# create conflicting line file on master
$ echo "roses are blue" > a.txt
$ git add .
$ git commit -m'blue'

# create conflicting line file on develop
$ git checkout develop
$ echo "roses are red" > a.txt
$ git add .
$ git commit -m'red'

# merge branches
$ git checkout master
$ git merge develop
Auto-merging a.txt
CONFLICT (add/add): Merge conflict in a.txt
Automatic merge failed; fix conflicts and then commit the result.

# investigate branch
$ git status
On branch master
You have unmerged paths.
  (fix conflicts and run "git commit")
Unmerged paths:
  (use "git add <file>..." to mark resolution)
	both added:      a.txt
no changes added to commit (use "git add" and/or "git commit -a")
```

## Looking into merge conflict
Don't think about merge conflict as something bad happed. Actually, merge conflicts save yours ass! To resolve merge conflict we will have to investigate where it occured. Lets have look into that.

```shell
$ cat a.txt
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

```shell
# edit, save and display content of conflicting file
$ vim a.txt
$ cat a.txt
roses are red

# commit changes
$ git add a.txt
$ git commit -m'resolving red/blue conflict'
[master b36c3a7] resolving red/blue conflict

# check the log
$ git log --oneline
b36c3a7 resolving red/blue conflict
4c2b42a red
8f2fbbd blue
d296a37 d.txt
166e350 init -readme.md
```

Tap yourself in the shoulder and shout Wunderbar!, because you just resolved yours first merge conflict.

## Amend
Sometimes you will find yourself in the situation where you forgot to add something important to the last commit, and the thing is not worth it to create new commit. This is where `git commit --amend` comes with help.

```shell
# amend text
$ echo "sky is blue" >> a.txt
$ git add a.txt
$ git commit --amend

$ cat a.txt
roses are red
sky is blue

$ git log --oneline
1a0f541 resolving red/blue conflict
4c2b42a red
8f2fbbd blue
d296a37 d.txt
166e350 init -readme.md
```
**Important!** This is the first time that we can notice that git actually does the **snapshots**. Have a look at the hash associated with last commit before and after `git commit --amend`. You can see that Git generated new hash -and this is the new snapshot.   

## Stash
Writing a software is a task that requires a focus. You have to go into the focus zone and start translating a conceptual models (requirements) into tangible things understandable by a computer. More likely, during process of writing code you will be interrupted, and request to fix some bug that appeared in previous commit(s). `git stash` is the tool that solves exactly this problem. It does what it says. It stashes uncommitted changes, and place you at the **HEAD**. Lets put our hands on it.


```shell
# we start working on some new feature
$ echo "I am in the zone" >> a.txt
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   a.txt

no changes added to commit (use "git add" and/or "git commit -a")

# your colleague comes and ask you to fix a bug
$ git stash
Saved working directory and index state WIP on master: 1a0f541 resolving red/blue conflict
HEAD is now at 1a0f541 resolving red/blue conflict

# check if something is stashed
$ git stash list
stash@{0}: WIP on master: 2289968 resolving red/blue conflict

# check that there is nothing to commit
$ git status
On branch master
nothing to commit, working directory clean

# now you do the fix and create commit;
$ touch b.txt
$ git add b.txt
$ git commit -m'b.txt'

# once you fixed the bug you can comeback to what you started
$ git stash apply
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   a.txt

no changes added to commit (use "git add" and/or "git commit -a")

# check that we are back on track
$ cat a.txt
roses are red
sky is blue
I am in the zone
```

## Discarding uncommitted changes
Sometimes you will find yourself in a situation that you will have to discard changes that you have started working on. To do it you will use `git check` command.

```shell
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   a.txt

no changes added to commit (use "git add" and/or "git commit -a")

$ git checkout a.txt

$ cat a.txt
roses are red
sky is blue
```

## Discarding committed changes
Often you will find yourself in the situation that you committed some changes that you will have to discard. No stress here. With Git you are able to discard discards commits as well.

To discard commit you have to copy **hash** associated with it and run `git reset --hard <commit_hash> `

```shell
# list project content
$ ls
a.txt  b.txt  d.txt  readme.md

# display commits
$ git log --oneline
e77b71d b.txt
1a0f541 resolving red/blue conflict
4c2b42a red
8f2fbbd blue
d296a37 d.txt
166e350 init -readme.md

# reset git repository to second the last commit
$ git reset --hard 1a0f541
HEAD is now at 1a0f541 resolving red/blue conflict

$ ls
a.txt  d.txt  readme.md

$ git log --oneline
1a0f541 resolving red/blue conflict
4c2b42a red
8f2fbbd blue
d296a37 d.txt
166e350 init -readme.md
```

As you can see we removed one commit by reseting the git repository to second the last commit. In other words we just removed leave form our branch :)

## Restoring deleted files
All of us knows what happens when you run this command `rm file.txt`. With the moment of pressing enter the file will be completely removed.

```shell
# display content of directory
$ ls
a.txt  d.txt  readme.md

# uppppps! files are gone
$ rm *

# display content
$ ls
$

# status
lukas@home:~/git-workshop$ git status
On branch develop
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	deleted:    a.txt
	deleted:    d.txt
	deleted:    readme.md

# checkout uncommited changes
lukas@home:~/git-workshop$ git checkout a.txt d.txt readme.md
lukas@home:~/git-workshop$ ls
a.txt  d.txt  readme.md

# status
lukas@home:~/git-workshop$ git status
On branch develop
nothing to commit, working directory clean
```

Zum teufel! Did it happen what I think it happened? Yes you just experience the misterious ***Forece*** that was first introduce to in **Episode IV** (1977).

Because git constantly tracks for the changes added and removed to your project and instantly creates snapshot of the changes at any time you rare able to commit or discard the changes. In this case our change was action of remove the files, which we discarded with `git checkout` command.

## Gitignore
Sometimes project that you are working on creates a files that are important to environment but not to the sourcode. An example of such case might be log files. With Git we are able to discard files or event whole directories (subdirectories) and its content if we wish to.

To discard files or directories in git you will have to create `.gitignore` file. Inside of this file you will add rules -which are understandable by git. This rules will be applied before every commit that you will create.


```shell
# create .gitignore with two rules
$ echo  '!.gitignore' > .gitignore
$ echo  '*.log' >> .gitignore
$ git add .
$ git commit -m'adding .gitignore'

# crate dummy log file
$ echo "test" > git.log
$ ls
a.txt  d.txt  git.log  readme.md

# status of the repository
$ git status
On branch develop
nothing to commit, working directory clean
lukas@home:~/git-workshop$
```

Yes, `git status` displays correct message. This is what our rules says.

* **!.gitignore** - don't ignore *.gitignore* files
* **\*.log** - ignore all files that ends with *\.log*


## Submodules
I've never seen a project that would not dependent on some 3rd party software. With Git you can include someone else software using submodules. Submodule/Module is a reference to an external Git repository reflected within the software.

Lets add our first submodule to our project

```shell
$ mkdir vendors
$ git submodule add https://github.com/sebpearce/bullshit vendors/bullshit
```  

From time to time you will have to update Git submodules. To do it execute bellow instruction.

```shell
$ git submodule update --recursive
$ git submodule update --recursive --remote
```

# Conclusions
Together we went through the most essentially skills that you need to have in order to work on a large projects. However, I didn't show you everything what git has to offer. I encourage you to explore Git more into deep by checking below resources.

But for now holding in one hand some bewski and in other Git's manual in shape of pretzel lets shout out the truth that we discovered that **Git ist GIT!!!**

* [Learn Git](https://www.atlassian.com/git/tutorials)
* [Git Docs](https://git-scm.com/doc)
