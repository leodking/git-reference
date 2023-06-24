# Resolving merge conflicts
Let's say we have a file called `foo.txt`. We're going to introduce a **merge conflict** to see how we resolve it. First, switch onto `master` branch, and from there create a new branch called `dev`:

	$ git checkout master
	$ git branch dev
	
Now make an edit to foo.txt on master branch, add it and commit it. Next, switch to `dev`:

	$ git checkout dev
	
And make some edits to foo.txt in the same place (e.g. if you changed line 2 on the master branch, change line 2 on the dev branch.) Add and commit those changes as well. You should have a tree looking something like this:

![[Pasted image 20210623162637.png]]

Now switch back to the master branch, and merge with the dev branch. You should see a conflict:

	$ git checkout master
	$ git merge dev
	Auto-merging foo.txt
	CONFLICT (content): Merge conflict in foo.txt
	Automatic merge failed; fix conflicts and then commit the result.
	
We can see this conflict in several ways. The first is through git status:

	$ git status
	On branch master
	You have unmerged paths.
	  (fix conflicts and run "git commit")
	  (use "git merge --abort" to abort the merge)

	Unmerged paths:
	  (use "git add <file>..." to mark resolution)
			both modified:   foo.txt

	no changes added to commit (use "git add" and/or "git commit -a")
	
Note the instructions: it's possible to "abort" the merge and go back to normal through `git merge --abort`. We can also see that something interesting is happening in gitk:

![[Pasted image 20210623163858.png]]

The green dot shows that there are staged changes which are not yet committed - this is the "Unmerged path foo.txt", or an indication of the merge conflict. We also have a red dot, indicating that we have local changes which are neither committed nor checked into the index. These changes were created by Git, and we can see what Git has done to help us resolve the Merge conflict here:

![[Pasted image 20210623164105.png]]

We can see this without the GUI if we use cat:

	$ cat foo.txt 
	foo
	<<<<<<< HEAD
	The contents of foo is in this file.
	=======
	This is the contents of foo.
	>>>>>>> dev
	
Git sees two conflicting lines - the one below "HEAD", which we added from `master`, and the one above `dev`, which came from the `dev` branch. Unlike in a three-way merge, Git has no ability to guess which version is correct, so you have to tell it.

You can either delete the lines you don't want to keep - including the `<<<<<<< HEAD`, `=======` and `>>>>>>> dev` - or if you're using a GUI tool like Visual Studio Code, press the button to accept the changes you want. Notice from above that VSCode has helpfully labelled which version is the `Current Change` and which is the `Incoming Change` - this will help us to decide which version we want to keep.

In my case, I pressed the button on VSCode to "Accept Current Change", and that handled the rest for me, deleting the other lines. This is the result.

![[Pasted image 20210623164524.png]]

Now we've fixed all of our conflicts, so we can add our file. Let's see what happens:

	$ git add foo.txt 
	$ git status
	On branch master
	All conflicts fixed but you are still merging.
	  (use "git commit" to conclude merge)

	Changes to be committed:
			modified:   foo.txt

This helpfully informs us that we have one more stage to go before we can finish the merge - committing. This will create a merge commit.

We can also see from gitk that there are no uncommitted changes:

![[Pasted image 20210623164725.png]]

Now we commit:

	$ git commit   

And we get the following message, which we can accept by saving vim using `:wq`:
  
	Merge branch 'dev' into master

	# Conflicts:
	#       foo.txt
	#
	# It looks like you may be committing a merge.
	# If this is not correct, please remove the file
	#       .git/MERGE_HEAD
	# and try again.
	
That leaves us with:

	[master 677e872] Merge branch 'dev' into master
	
Git status comes out clean, so we'll see gitk:

![[Pasted image 20210623165149.png]]
	


#git