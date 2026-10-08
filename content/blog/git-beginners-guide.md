+++
title = "How to Use Git (and the CLI!) for a complete beginner (linux guide)"
date = 2026-10-06
description = "git user guide for the uninitiated"
[taxonomies]
tags = ["linux", "git"]
+++

> NO AI WAS USED IN ANY PART WRITING, EDITING, OR FINISHING THIS GUIDE.
> ENJOY!

# How to Use Git (and the CLI)
*this is especially directed towards hackclubbers. if you don't know what that is and are 18 or under, i'd reccommend checking hackclub.com out :P*
#### this is oriented towards *complete* beginners, meaning if you already know how to use a command line or know how to use linux, this guide is either not for you, or you can skip pretty far ahead. enjoy!

> if you do not have a GitHub account, please make one,
and then come back to this tutorial. this will **not** cover
how to make a github account, but will expect you to have one.

## what is git?
[Git](https://git-scm.com/) is a tool that allows you to track, manage and save multiple different versions of your code.
[GitHub](https://github.com/) is (one of) the most popular web frontends/code hosting platforms, and users,
(like you at the end of this guide!) use it to store and share their code with the world.
they use Git to do so. Hack Club *requires* people to use github to host their code/projects to participate/submit to their events.

## installation

### Linux
for linux, it's almost always installed by default, but if it isn't you probably can install it,
either by a quick visit to [the Linux installation page](https://git-scm.com/install/linux), or however you normally install packages

### MacOS or Windows
since i don't use either of these, it's hard to tell you how to install it.
I reccommend reading the page for either
1. [Windows](https://git-scm.com/install/windows), or
    - you can also just use WSL and install git in whatever linux environment you have in there too
2. [MacOS](https://git-scm.com/install/mac)

## intro to Git Bash / the command line
ok. so *if* git installed correctly, you should be able to open an app (in windows)
called "Git Bash". get used to this app, because you will be spending a lot of time in it.

### a short aside
note: this is written without access to a windows computer, so take all windows-specific things witha  grain of salt

#### what is this app?
this is basically Git's way of creating linux in windows without creating linux in windows :P
don't dwell too much on that, because it's not really necessary to know/care about lol
 (unless ofc you use linux daily and are on windows for some strange reason in which case,
 this is *one of* the best ways to use "linux" on windows :p)

### what's a 'command line'?
a command line is where you will be interacting with git, and manipulating files,
and folders, etc. 

#### some basic commands
on the command line (specifically git bash if you're on windows),
one of the commands you will be using the most is `cd`. `cd`
is short for 'change directory'. you type `cd [directory name]` 
to change the current directory to the directory of `[directory name]`.  

*'directory' is just another word for folder, by the way.*

another few commands to get used to are `ls` and `mkdir`. `ls` lists all files in
the current folder, and `mkdir` makes a new folder taht you can then
`cd` into.
also, another one you will see me use is `touch`. `touch` just makes a blank file with whatever name you give it, like `touch README.md`, etc.
I reccommend trying this out. make a new folder, and open it in git bash.
then try running these commands or something similar:
```bash

# NOTE: in all of these, just input what is after the dollar sign
# into your command line.
# first, create a directory...
new-directory $ mkdir newest-dir
#then 'cd' into it...
new-directory $ cd newest-dir
# right here it should change to the directory you created...
# and now we are in your created directory! now for git!
newest-dir $

```

Okay. now after that, we are ready to start using git!

## Our First Git Commands and Project!
now that you have an (albeit basic) understanding of the command line and a few basic commands, you are ready to start learning how to use the git CLI. the Git CLI is notoriously hard to use, but don't worry, we will get through this together!

first, we want to have git start tracking our files. the command that i'm about to show you is the very first command that you need to run in every future project that you want tracked by git/up on github.

just run these commands in your `newest-dir` folder. (in git bash, or the terminal)
```bash

# initialize the tracking, also called a repository.
newest-dir $ git init
# that should display some sort of warning message about 'branch name'
# or something like that, don't worry about it.
```
now that you have you git tracking turned on or enabled for this folder,
open the `README.md`file from earlier in a text editor and write something in it.
(you can use any text editor you want, but i recommend VSCode :P )

after that, come back here and follow these commands:
``` bash

# now, since you have made changes to the README, you can now
# track it using git! this is pretty straightforward, you just have to
# 'add' it to the tracking. you can with the following command:
newest-dir $ git add README.md
# it added it to the tracking! the next step is to 'commit', or just finalize
# your changes by running 'git commit':
newest-dir $ git commit -m "initial commit!"
# it should print some stuff about 'create mode' and also say 'initial commit!'
# somewhere too.

# you can replace the message inside the quotes with whatever you want.
# I just use 'initial commit' because it helps me see that this is the first
# commit.
```

congrats! you just committed your first file!

*if/when you make more changes, you just need to run the `git add [file_name]` and `git commit -m "[message]"`, with [file_name] and [message] replaced with the file name and message respectively.*

Here, let's see an example of that.
say you added a new file named `foo.html`. 
you want `foo.html` to be tracked as well, right? well, to add `foo.txt` to the tracking,
all you need to do is do `git add foo.txt` (along with `git add README.md`
if you changed it from last time you committed). but, what if you have many many files in subfolders, etc? you could name all files you want in one `git add`, like so: 
```bash 
git add README.md foo.txt #etc...
```
*OR*

you could do this instead:

```bash
git add .
```

this command adds *every* single file in you current directory and all subfolders. (this means you have to be at the top of your project to run this command, not in a folder inside it.

*this is what i will be referring to and using for the remainder of the guide.*


### Pushing to GitHub

> note: in this part, i will be referring to new content that might be slightly hard
to understand. that is okay. just follow what i'm doing and by the end of this, you should be good to go for future projects!

#### Setting up SSH on GitHub
to get this to work, we first need to set up an 'SSH Key' on GitHub so GitHub knows
exactly what computer is yours and who is trying to push code onto their website.

to set up SSH keys on github we first need to generate an SSH key.

I like to direct you to [this](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent?platform=windows#generating-a-new-ssh-key)
url, it's a wayyyy better and more concise guide than i could write lol.
once you get to the 'adding SSH key to SSH-Agent', come back here because you don't have to do that part.

ok. now you have an SSH key on your system. congrats! you are halfway there. now you just need to add it to github.

so, to do that, you need to first copy the contents of your `id_ed25519.pub` file.
run this command and copy the output:
```bash
$ cat ~/.ssh/id_ed25519.pub
```
> just copy that to your clipboard for this next part

then, go to GitHub, and in the upper top right, click on your profile picture and select 'settings'.
please then select 'SSH and GPG Keys' from the sidebar to the left.
click 'Add SSH key' or 'New SSH Key'.
select the type of key, for this one, select 'authentication'.
in the 'key' field, paste the key you copied earlier.
click 'add ssh key'.
you might heve to enter your password too, but once you do, you will be ready for the next step!!

