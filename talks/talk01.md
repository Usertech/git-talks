title: GIT talk 01
author:
  name: Lukáš Rychtecký
  twitter: lukasrychtecky
controls: true
style: style.css

--

# GIT for dummies
## Talk 01
## Lukáš Rychtecký
## [https://twitter.com/LukasRychtecky](https://twitter.com/LukasRychtecky)

--

### Outline

* Motivation
* First steps
* Base commands
* Myths and lies
* References

--

### Motivation - Task

#### Task: Write an essay

* First day: `my-essay.txt`
* Team work

--

### Motivation - Day 2

* `my-essay.txt`
* `my-essay2.txt`

--

### Motivation - Day 5

* `my-essay.txt`
* `my-essay2.txt`
* `my-essay-2016-01.txt`
* `my-essay-final.txt`
* `my-essay-final2.txt`

--

### Motivation - What file?

![What file?](http://cdn.meme.am/instances/42603185.jpg)

--

### Motivation - Go deeper

#### You have to put together this:
* `my-essay2.txt`
* `my-essay-2016-01.txt`
* `my-essay-final.txt`
* `my-essay-final2.txt`

#### With that:
* `tom-essay3.txt`
* `tom-essay-final3.txt`

--

### Motivation - Merge two files

![Merge two files](https://backlogtool.com/git-guide/en/img/post/intro/capture_intro1_1_2.png)

--

### What is GIT?

Git is distributed version control system

* Keeps every saved change (commit/version) of your text files
* Allows to backup any version from history
* Syncs with remote computers (repositories)
* Works offline (no Internet needed)
* Easy team work
* Much more ...

--

### We love GIT

![Use Git](http://i.qkme.me/3u48x0.jpg)

--

### GIT - First commit

* Create a file `a.txt` and put a text into it
* Save a version with Git write
  * `git add a.txt` - saves current version of `a.txt`
  * `git commit -m "First draft of Git talks"` - makes new version with message
* Done!

--

### GIT - What is changed

* Add few paragraphs into `a.txt`
* `git status` - shows what is changed, output willl be like

```bash
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    modified:   a.txt
```
--

### GIT - What are changes

* `git diff` - see the changes, output will be like:

```bash
diff --git a/a.txt b/a.txt
index 796d523..497812f 100644
 --- a/a.txt
 +++ b/a.txt
@@ -1 +1,3 @@
 This is a greate talk!
+
+More more Git!
```

* `git add a.txt` - adds a file into an upcomming commit
* `git commit -m "First Git talk is done."`- creates new version

--

### GIT - What is done

* Let's see what is done - `git log`, output will be like:

```bash
commit 55f21e56db012484919cef1a1f196ffb9aea1915
Author: Lukas Rychtecky <lukas.rychtecky@gmail.com>
Date:   Wed Jan 27 19:25:39 2016 +0100

    First Git talk is done.

commit a4f7d624255cc36676f252355326195d6fdda602
Author: Lukas Rychtecky <lukas.rychtecky@gmail.com>
Date:   Wed Jan 27 19:14:14 2016 +0100

    First draft of Git talks
```
--

### GIT - Backup changes

* Let's send the changes into a remote computer (repository) and save work - `git push`
* The remote repository can be in the Internet and our work is safely backuped
* Download changes from the remote repository - `git pull`

--

### Commands - Commit

* Creates new version
* A commit message is needed
* The message has to describe **what is done**! - IMPORTANT
* Keep commit **smallest as possible** - IMPORTANT
* Has a unique ID - that weird long string like `55f21e56db012484919cef1a1f196ffb9aea1915`

--

### Commit message

![Commit message](http://cdn.meme.am/instances/55072437.jpg)

--

### Commands - Add and status

#### Add

* Prepares a files for an upcomming commit
* Says to Git `Hey I want to safe this file`

#### Status

* Shows what files are changed

--

### Commands - Log

* Shows a full history of all changes
* Easy filtering via date, author etc.

![Git for everyone](https://i.ytimg.com/vi/CDeG4S-mJts/hqdefault.jpg)
--

### Commands - Push and pull

#### Push

* Pushes commits into a remote repository
* Repositories could be anywhere (connected into a network)

#### Pull

* Downloads commits from a remote repository
* Merges changes with your teammates

--

### Commands - Help

#### I'm lost!

![Need help](http://i0.kym-cdn.com/entries/icons/original/000/009/993/tumblr_m0wb2xz9Yh1r08e3p.jpg)
* try `git help` or `git help <command>`
* Google

### Myths and lies

* GIT is only for programmers
* Commands are super-nerdy complicated [https://tortoisegit.org/](https://tortoisegit.org/)
* Git has deleted my work! (almost impossible!)

--

### Summary

#### Commands

* `add` - prepares files for a commit
* `commit` - makes new version
* `pull` and `push` - syncs with remote repositories
* `status` - shows what is changed
* `diff` - shows changes
* `log` - shows a history

--

### References

* `man git` or `git help`
* https://git-scm.com/ - official website
* [Pro GIT](https://git-scm.com/book/en/v2) - ask me for czech version in PDF
* Git guide - https://backlogtool.com/git-guide/en/
* Git game (advanced) - [http://pcottle.github.io/learnGitBranching/](http://pcottle.github.io/learnGitBranching/)

--

### Thanks for your attention

![Linus Torvalds](http://cdn.meme.am/instances/22164438.jpg)
