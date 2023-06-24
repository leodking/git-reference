Get the difference between two files

	echo "foo" > example_file.txt
	git diff

by default, git diff shows the difference between the working directory and the **index** (staging area), i.e. all changes marked "Changes not staged for commit"

You can diff commits:

	git diff 13232a 12232f

Or branches:

	git diff main feature

Or you can diff a file in the working directory to the local repository:

	git diff HEAD example_file.txt

This compares example_file in the local directory vs in the local repository. 

If I use the below it will compare all changes of **tracked files**

	git diff HEAD

If I add a file which is **not** checked into the local repo, then git diff will not show it using the above command because it's not checked in. e.g.

	echo "new foo" > new_file.txt
	git diff
	git add new_file.txt
	git diff
	git commit -m "Add new file"
	git diff

But if I make further modifications to it THEN it will show up:
	
	echo "bar" >> new_file.txt
	git diff
	diff --git a/new_file.txt b/new_file.txt
	index f0d808f..31275ce 100644
	--- a/new_file.txt
	+++ b/new_file.txt
	@@ -1 +1,2 @@
	 new foo
	+bar

Because the file is tracked in the local repo

## Diff against remote

	git diff master origin/master
	git diff <local branch> <remote>/<remote branch>

To do this you need to git fetch first - you must have accurate info about the remote.

## Which order does git diff work in?

Okay. Let's say I have two versions of a file called `myfile`:
1st version, which I commit:

	Line 1
	Line 2

2nd version, which I commit later:

	Line 1
	Line 2
	Line 3

I check 'git log --graph'

	$ git graph
	* c7ff3be - (2 minutes ago) 2nd commit - Leo King (HEAD -> master)
	* e424622 - (3 minutes ago) 1st commit - Leo King

So c7... is the second commit (Line 3), e4... is the first commit (no Line 3). Let's say I do:

	$ git diff c7ff3be e424622
	diff --git a/myfile b/myfile
	index 6ad36e5..c82de6a 100644
	--- a/myfile
	+++ b/myfile
	@@ -1,3 +1,2 @@
	 Line 1
	 Line 2
	-Line 3

It shows here as a subtraction - I'm taking **AWAY** Line 3. So with 2nd commit as the first and 1st commit as the 2nd, it's showing the wrong order ... I think. I want to do it the other way around to know what's been changed.

	$ git diff e424622 c7ff3be
	diff --git a/myfile b/myfile
	index c82de6a..6ad36e5 100644
	--- a/myfile
	+++ b/myfile
	@@ -1,2 +1,3 @@
	 Line 1
	 Line 2
	+Line 3

![[Pasted image 20220316094716.png]]

The second output correctly shows that Line 3 was added, not removed. 

So for correct diffing, the first argument must be the base or the thing we want to compare against. The second is the thing we want to see the changes in.