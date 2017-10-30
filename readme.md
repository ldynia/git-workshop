
<a href="https://www.youtube.com/watch?v=Q37xJtuQ24w&t=1m11s">
  <p align="center">
    <img src="too_old.png"/>
  </p>
</a>

# Das ist GIT!
Welcome to the `Git version control` workshop. Objectives of this workshop are to teach you concepts encountered in version control tools, as well as to give you necessary [Git](https://git-scm.com/doc) skills that you will apply in your next project. Tutorial was written with focus on people who has none or limited knowledge of Git.

In this tutorial I will walk you through basic commands that you have to know, and tasks that you will perform while working with Git. Enough talking,let's started our project.

## Requirements
Before starting this tutorial you have to fulfilled below requirements.

* [git](https://git-scm.com/) - installed
* [vim](https://vim.sourceforge.io/) - installed
* [github](https://github.com/) or [gitlab](https://about.gitlab.com/) or [bitbucket](https://bitbucket.org/) - account
* access to a linux/unix terminal

## Assumption
I assume that a reader has fulfilled points specified in requirements section.

## History
Let me ask you this question. Try to name a single software that has the grates impact on humanity? it's difficult one, but in my opinion it's [Linux](https://en.wikipedia.org/wiki/Linux) initially written by [Linus Torvalds](https://en.wikipedia.org/wiki/Linus_Torvalds).

Without Linux, you would have to throw out all smartphones, tablets and TVs that run on Android and iOS. Moreover, content of the web would shrink at least 65% and many more.

But how you write a software that counts 15+ million lines of code? For suer, it can't be written by a single man. Further more in the project like this you would like to keep track on who added changes, when changes had been added, what was added, which files had been removed, recover deleted files, resolve overlaps of conflicting information, version the changes, fix bugs, fix security volubilities etc.

Another brilliant thing that Linus Torvalds wrote for the purpose of facilitating development of the Linux kernel was [Git](https://en.wikipedia.org/wiki/Git). Today Git is the most popular `version control` / `source control` software used by developers. So, if you didn't use any [version control](https://en.wikipedia.org/wiki/Version_control) tools then I have pity on you!

OK, if the thing that I'm writing about doesn't make sense to you then don't worry. I will walk you through the various use-cases of using Git.

## Vocabulary
To makes things easier let's level up and gain necessary vocabulary to work with git.
* **remote** - refers to git repository hosted in the cloud.
* **origin** - refers to branch on remote.
* **branch** - direction of work within your git repository.
* **master** - default branch for any git repository.
* **commit** - amount of information to be contributed to a branch.
* **push** - action of sending commits to origin (cloud).
* **pull** - action of retrieving commits from origin (cloud).
* **HEAD** - latest commit on active branch.

## Inner Workings
Git thinks of data as a set of snapshots. Every time you create a commit, or save the state of your project, Git takes a picture of all files stored in your project and reference to it as snapshot (commit). If files have not changed then Git doesn’t store the file again, instead it links to the previous identical file it has already stored. However, if a file has changed then Git stores the difference between previous state of the file and the current state.

Every time you create a commit Git creates a snapshot represented by SHA-1 hash (cheksum), this way it's impossible to change content of a file without Git knowing about it. Additional advantage of using Git is possibility of working offline. You can locally contribute changes to your project and next time when you are online you will sync the difference between your local version of the project with online version.

## Conceptual model
The key to understand anything new is to develop conceptual model about the thing that you try to learn. A good conceptual model should be easily explainable to a kid. If you can do that then, it means that you have a big picture of the thing that you are talking about, *und das is GIT! Ja?*

### The tree
One way of thinking about version control is to associate it with a tree. Every tree has many branches that originate in common root. Moreover, a branch has many leaves that grow along the branches.

The essence of working with version control is basically to create branches and leaves. A branch symbolize development path or a direction of work. A leaf is a contribution to the branch it can be a line(s) of code, or a segment of text. It can be even a number of bytes introduce to binary file.

## Git config
Before we start working with Git we have to configure it first. Let's add basic information associated with our Git user such  a **username** and an **email**. **Remember to set appropriate username and email to yours account !!!**  

```shell
$ git config --global user.username "T800"
$ git config --global user.email "T800@skynet.com"
```  

## Git local repository
**Git repository** is a **.git** folder located within yours project directory. The **.git** folder is a hidden directory that contains git's files. Git files track changes to all files within your project.

Let's create our first project and within the project we will create our first Git repository. We will refer to this repository as a **local repository** because it will reside locally on our machine.

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
**Remote** Git repository is nothing more than your local Git repository uploaded to the cloud (**remote**).  The most used cloud for Git repositories is [github.com](https://github.com/), and we will work with it. However, feel free to work with any source code management service (cloud).

To create a **github repository** do as follow

1. Go to [github.com](https://github.com/)
2. Sign in
3. Clink button called **new repository**
4. Enter project name called **git-workshop**
5. Click button called *Create repository*
6. Click button called *Https* and copy repository's url. **Remember to change user name to your's github username!!!** eg. `https://github.com/ldynia/git-workshop.git`

Voila, we created our first remote Git repository!

## Binding local with remote
Now what left to do is to bind **local** (offline) repository with **remote** (online). Execute below command within `git-workshop` directory. **Don't forget to change username in repository url!!!**

```shell
$ git remote -v
$ git remote add origin https://github.com/ldynia/git-workshop.git
$ git remote -v
origin	https://github.com/ldynia/git-workshop.git (fetch)
origin	https://github.com/ldynia/git-workshop.git (push)
```

## Commit
If we think about process of developing a program (writing a code) then, it's nothing more than adding/removing/updating/renaming a files and directories.

Saying that let's contribute first file to our project and create our first commit. You gonna do this step a million times!

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
At any time you can see the history of changes contributed to a Git repository. To do so execute `git log` command. The log is displayed top down -top being the newest commit, down the oldest.

```shell
$ git log
commit 166e35068dd1642ef21a72ce77ea4056f73c45a0
Author: ldynia <ludd@cbs.dtu.dk>
Date:   Tue Sep 12 11:15:56 2017 +0200

    init -readme.md
```

As you can see single log contains four elements.
* **hash** - unique identifier of commit (SHA-1).
* **author** - person who contributed changes.
* **date** - time of contribution.
* **message** - message associated with commit.

I have to admit that `git log` doesn't display information in the nicest way. My favourite tool for working with git log is [tig](https://jonas.github.io/tig/). I highly recommend to install it.

## Push
Going with the flow, the next step is to upload our first commit to the cloud (`remote`). We can achieve it with `git push` command. **Remember to change your user name!!!**.

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
Root of the tree is **master** branch. Eventually all branches merge into it.

The real deal working with version control tools is to create multiple branches (unless you work for Google). The common scenario is to have a **master**, **develop**, **testing** branch that will be deployed to equivalent environment.

Let's create a **develop** branch which roots from a **master** branch.

```shell
# create new branch
/Coding/workshops/git-workshop$ git checkout -b develop
Switched to a new branch 'develop'

# display all available branches
$ git branch
* develop
  master
```

The **\*** (asterisk) next to branch name indicates that **develop** branch is our active branch. Other words we are working on **develop** branch now.

Let's commit a new file into **develop** branch and checkout to the master branch and investigate content of our directory.
```shell
# create commit on develop branch
$ touch d.txt
$ git add d.txt
$ git commit -m'd.txt'
[develop 1a627dc] adding dev file
1 file changed, 0 insertions(+), 0 deletions(-)
create mode 100644 d.txt

# list files
$ ls
d.txt readme.md

# checkout to master branch and list content of directory
$ git checkout master
Switched to branch 'master'

# list files
$ ls
readme.md
```
Wait the moment. What the hell happened? Are we missing a file along with the 18 minutes of Watergate? Didn't we create a file few seconds ago? Yes we did. Hold your horses and don't panic the file is still there. What happened is, we created a file (commit) on the **develop** branch and we switch the branches. Because of two different snapshots stored on branches the **master** branch is behind the **develop** branch, and because of that we cannot see the file on **master** branch.

Too much talking let's have a loop at it.

```shell
$ git checkout develop
Switched to branch 'develop'

# files are still here
$ ls
d.txt  readme.md
```

Now let's see the history of our work using `git log` command.

```shell
# list history of commits
$ git log --oneline
d296a37 d.txt
166e350 init -readme.md
```

Things look OK aren't they? Let's see the commits on the master branch.

```shell
$ git checkout master
Switched to branch 'master'

$ git log --oneline
166e350 init -readme.md
```
Can you see now that we are behind one commit on the **master** branch? This commit contains our file, we will be able to include it into master branch wit `git merge` command.

## Merge
Another thing that you will be doing frequently with git is to merge a commits between the branches -I'm telling you that you will be bored with it. To merge changes from one branch to another you have to switch to the branch that you want to merge changes into and execute `git merge <branch_tom_merge_with>` command.

```shell
# change branch
$ git checkout master
Already on 'master'

# merge with develop
$ git merge develop
Updating 166e350..d296a37
Fast-forward
 d.txt | 0
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 d.txt

# display log
$ git log --oneline
 1a627dc adding dev file
 aec47ab init -adding readme.md

# display content
$ ls
d.txt  readme.md
```

## Merge conflicts
  So far so good. However, things not always go as expected. Often you will find yourself in a situation where you'll have to resolve **merge conflicts**. A conflict in context of version control is a situation when you try to merge a files that has overlapping content between the branches that you are trying to merge. Here is an example.

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
Don't think about merge conflict as something bad happen. Actually, merge conflicts save your ass! To resolve merge conflict we will have to investigate where it occurred.

Let's have look into that.

```shell
# display content
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

The important thing to notice is the **HEAD** and the order in which the conflict is structured. Upper part that contains the **HEAD**, refers to current active branch - in our case it's the master branch. Lower part refers to branch that we are merging with - this time it's **develop** branch.

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

Tap yourself in the shoulder and shout Wunderbar!, because we just resolved our first merge conflict.

## Amend
Sometimes you will find yourself in the situation where you forgot to add something important to the last commit. However, the changes you are trying to add are not worth of creating new commit. This is where `git commit --amend` comes with help.

```shell
# amend text
$ echo "sky is blue" >> a.txt
$ git add a.txt
$ git commit --amend

# display content
$ cat a.txt
roses are red
sky is blue

# display log
$ git log --oneline
1a0f541 resolving red/blue conflict
4c2b42a red
8f2fbbd blue
d296a37 d.txt
166e350 init -readme.md
```
**Important!** This is the first time that we can notice that Git actually does the **snapshots**. Have a look at the hash associated with last commit before and after `git commit --amend`. You can see that Git generated new hash -and this is the new snapshot.   

## Stash
Writing a software is a task that requires a focus. You have to go into the focus zone and start translating a conceptual model (requirements) into tangible things understandable by a computer. More likely, during the process of writing code you will be interrupted, and request to fix some bugs that appeared in previous commit(s). `git stash` is the tool that solves exactly this problem. It does what it says. It stashes uncommitted changes, and place you at the **HEAD**. Let's put our hands on it.


```shell
# we start working on some new feature
$ echo "I'm in the zone" >> a.txt
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

# check that there is nothing to commit
$ git status
On branch master
nothing to commit, working directory clean

# check if something is stashed
$ git stash list
stash@{0}: WIP on master: 2289968 resolving red/blue conflict


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
I\'m in the zone
```

## Discarding uncommitted changes
Sometimes you will find yourself in the situation that you will have to discard changes that you have started working on. To do it you will use `git check` command.

```shell
# check status
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   a.txt

no changes added to commit (use "git add" and/or "git commit -a")

# discard changes
$ git checkout a.txt

# display content
$ cat a.txt
roses are red
sky is blue
```

## Discarding committed changes
Another thing that you'll often encounter is the situation that you committed some changes that you will have to discard. No stress here. With Git you are able to discard discards commits as well.

To discard a commit, you have to copy **hash** associated with it and run `git reset --hard <commit_hash> `

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

# list files
$ ls
a.txt  d.txt  readme.md

# display log
$ git log --oneline
1a0f541 resolving red/blue conflict
4c2b42a red
8f2fbbd blue
d296a37 d.txt
166e350 init -readme.md
```

As you can see we removed one commit by reseting the git repository to second the last commit. In other words we just removed leaf from our branch :)

## Restoring deleted files
All of us knows what happens when you run this command `rm file.txt`. With the moment of pressing enter the file will be gone.

```shell
# list files
$ ls
a.txt  d.txt  readme.md

# uppppps! files are gone
$ rm *

# list files
$ ls
$

# status
$ git status
On branch develop
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	deleted:    a.txt
	deleted:    d.txt
	deleted:    readme.md

# checkout uncommited changes
$ git checkout a.txt d.txt readme.md

# list files
$ ls
a.txt  d.txt  readme.md

# status
$ git status
On branch develop
nothing to commit, working directory clean
```

Zum teufel! Did it happen what I think it happened? Yes you just experience the mysterious ***Force*** that was first introduce to in **Episode IV** (1977).

Because git constantly tracks for the changes added and removed to your project and instantly creates snapshot of the changes at any time you are able to commit or discard the changes. In this case our change was action of remove the files, which we discarded with `git checkout` command.

## Tagging
Additionally interesting feature that Git has to offer is ability of tagging specific commits. Tagging is a convenient solution for marking milestones in software project.

Let's have a look at it.

```shell
# display all tags
$ git tags
$

# create tag
$ git tag -a 1.0 -m"1st stable version"
$ git tag -n

# push tags to remote
$ git push origin master --tags

# show tag
$ git show 1.0
tag 1.0
Tagger: ldynia <ludd@cbs.dtu.dk>
Date:   Thu Sep 21 11:30:33 2017 +0200

1st stable version

commit f999edd5140ace058849fcb8a68e8149fd4befe4
Author: ldynia <ludd@cbs.dtu.dk>
Date:   Thu Sep 21 11:15:36 2017 +0200

    adding .gitignore

diff --git a/.gitignore b/.gitignore
new file mode 100644
index 0000000..e28965b
--- /dev/null
+++ b/.gitignore
@@ -0,0 +1,2 @@
+!.gitignore
+*.log
```

## Diff
`git diff <filename>` is probably my favoirite command. It allows us to see difference between changes introduce in latest commit and changes on the **HEAD**. Actually, we even can do `git diff` on a file located at different branches.

Let's have a look at both cases.

```shell
# create even numbers on master
$ echo -e "1\n2\n4\n6" >>  numbers.txt
$ git add numbers.txt
$ git commit -m'even numbers'

# create odd numbers on develop
$ git checkout develop
$ echo -e "3\n5\n7\n9" >>  numbers.txt
$ git commit -m'odd numbers'

# compare numbers between branches
$ git checkout master
$ git diff master develop numbers.txt
diff --git a/numbers.txt b/numbers.txt
index 76fda2f..dd9c834 100644
--- a/numbers.txt
+++ b/numbers.txt
@@ -1,4 +1,4 @@
-1
-2
-4
-6
+3
+5
+7
+9

# compare diff between HEAD
$ echo "3.14" >> numbers.txt
$ git diff numbers.txt
diff --git a/numbers.txt b/numbers.txt
index 76fda2f..5b51314 100644
--- a/numbers.txt
+++ b/numbers.txt
@@ -2,3 +2,4 @@
 2
 4
 6
+3.14

# create commit
$ git add  numbers.txt
$ git commit -m'pi'
```

## Checkout from branches
Previously we worked with `git checkout` in the context of restoring/discarding changes. Now, we will use it to actually checkout changes introduced to a file on a different branch. You might ask yourself that previous sentence does sound like a `git merge`? And yes, it does. However, sometimes we might find ourself in the situation that we want to checkout a single file rather than whole branch.

Let's have a look at it.

```shell
# create commit
$ git checkout develop
$ echo "2.71" >> numbers.txt
$ git add numbers.txt
$ git commit -m'e'

# change branch and display content
$ git checkout master
$ cat numbers.txt
1
2
4
6
3.14

# cheery pick file
$ git checkout develop -- numbers.txt
$ cat numbers.txt
3
5
7
9
2.71
```

Opps! What happened? I tell you what happened. We just learn that using `git checkout` might be as risky as stepping on a thin ice. We literally **checkout** a file. By this, I mean that we replace content in `numbers.txt` on **master** branch, with content from `numbers.txt` on **develop** branch, without checking merge conflicts.

There is less pitfall way of checking out files from different branch. We just have to add `--patch` option and we will be prompted with question about what action should we take before checkout.


```shell

# reset branch to previous state
$ git reset HEAD
$ git checkout .

# checkout
$ git checkout --patch develop numbers.txt
diff --git b/numbers.txt a/numbers.txt
index 5b51314..df43dda 100644
--- b/numbers.txt
+++ a/numbers.txt
@@ -1,5 +1,5 @@
-1
-2
-4
-6
-3.14
+3
+5
+7
+9
+2.71
Apply this hunk to index and worktree [y,n,q,a,d,/,e,?]?
```
Pres `q` to quit checkout.


## Gitignore
Sometimes project that you are working on creates a files that are important to environment but not to the sourcode. An example of such case might be a log files. With Git we are able to discard files or even whole directories.

To discard files or directories in Git you will have to create `.gitignore` file. Inside of this file you will add rules -which are understandable by Git. This rules will be applied before every commit that you will create.


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
$
```

Yes, `git status` displays correct message. This is what our rules says.
* **!.gitignore** - don't ignore *.gitignore* files
* **\*.log** - ignore all files that ends with *\.log*


## Submodules
I've never seen a project that would not dependent on some 3rd party software. With Git you can include someone else's software using `git submodule` command. Submodule/Module is a reference to an external Git repository reflected within yours project.

Let's add our first submodule to our project

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
Together we went through the most essentially skills that you need to have in order to work on a large projects. However, I didn't show you everything what Git has to offer. I encourage you to explore Git more into deep by checking below resources.

But for now holding in one hand some brewski and in other hand Git's manual in the shape of pretzel. Let's shout out the truth that we discovered that **Git ist GIT!!!**

* [Git Docs](https://git-scm.com/doc)
* [Git Tutorial](https://www.atlassian.com/git/tutorials)
