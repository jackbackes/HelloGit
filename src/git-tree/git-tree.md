This is a quick tutorial on the git tree structure. At the end of this brief walkthrough, you'll have a program that looks like this:

![alt end-result](./git-tree-end.png?raw=true)

Let's figure out what this means!

From your terminal:
```bash
$ mkdir HelloGitTree && cd HelloGitTree
$ git init
#creates a new git repository!
$ git log 
#you'll get an error because there's nothing in your tree yet. that's ok!
$ touch example.txt
$ git status 
#example.txt will show as "untracked" in red
$ git add example.txt 
#"stages" example.txt for committing to the tree
$ git status 
#example.txt now shows up in green! sweet!
$ git commit --message="this is my first commit" 
#this adds example.txt to your tree
$ git log --graph --decorate --oneline --all 
#this is a great way to visualize your entire git repository. 
#right now you only have one commit
$ vim example.txt      
#opens vim text editor
```

```vim
i             
# puts vim into "insert mode"
"Hello World" 
# because why not?
esc           
# exits "insert mode"
:wq           
# saves and exits vim text editor
```

```bash
$ git status             
# `git status` shows you your current "working tree", in other words, 
# the files in your repository that have been modified but 
# haven't been committed yet.
$ git add example.txt # why does example.txt need to be added again?
# think of it this way - you are moving your CHANGES into the staging area
$ git status 
# now example.txt is green!
$ git commit -m "this is my second commit" 
# `-m` is shorthand for `--message=`
$ git log --graph --decorate --oneline --all
```
Now you have two commits in your tree. notice that code-thing (something like `4f3c80a`)? That's your commit id. each commit is like a link in a chain of changes from the beginning (in this log, the beginning is at the bottom and the end is at the top). `(HEAD -> master)` means that you are currently looking at your "master" branch, which is like the trunk of a tree, or the vine for your bushel of grapes. Right now you only have one "branch". Let's create another one.
```bash
$ git branch Goodbye
$ git log --graph --decorate --oneline --all 
# now you have two "branches," master and "Goodbye".
# Let's make "HEAD" point at Goodbye.
# Think of it this way: your eyes are in your HEAD - so you are LOOKING at that branch.
$ git checkout Goodbye 
# now "HEAD" points at the "Goodbye" branch.
# But right now Master and Goodbye are both pointed at the same commit.
# Let's change that.
$ vim example.txt
```
```vim
i
# replace "Hello" with "Goodbye"
esc
:wq 
#this saves
```
```bash
$ git commit -a -m "My third commit" 
# if you want to commit all your changes,
# you can skip "add" by using the '-a' option
$ git checkout master
$ vim example.txt 
# where did our changes go?
```
```vim
:q!
```
```bash
$ git checkout Goodbye 
$ vim example.txt 
# oh there it is
```
```vim
:q!
```
```bash
$ git checkout master
$ vim example.txt
```
```vim
i
# ...make a bunch of changes...
esc
:wq
```
```bash
$ git commit -am "BLOW UP THE WORLD"
$ git log --graph --decorate --oneline --all 
# hey, now it looks like a real tree... maybe a cactus...
```
ok, now here's some magic...
```bash
$ git diff Goodbye master 
# should look something like this:
```
now let's say I want to go back to where I was, to our original "Hello World" commit. I'll need the "commit id" of the version of the "tree" that I want.
In this case, the "commit id" is 4f3c80a. You'll have to run the "git log" command above to find the commit id (which is unique and will be different on your computer).
We could just run "git checkout 4f3c80a". But I'd like to create a new branch so it's easy to get back. So run this command:
```bash
$ git checkout -b Hello 4f3c80a 
# use your commit id instead of 4f3c80a.
```
now run git log again:
```bash
$ git log --graph --decorate --oneline --all
```

remember, "HEAD -> Hello" means I'm looking at the Hello branch. The Hello branch points to commit 4f3c80a and everything below it.
```bash
$ git diff Hello Goodbye 
# this shows the changes that need to be made to get from Hello to Goodbye.
# Remove "Hello World!" and add "Goodbye World!"
```


I haven't gotten into remote repositories, etc, because there are plenty of resources on that. To me, understanding the tree structure is key to git.
