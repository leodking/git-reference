# git stash
Let's say we make changes to a working directory and don't add or commit those changes. This is not, in other words, a "clean" working directory. I've added some text to `foo.txt`, and when I do `git status` it will show this:

	On branch master
	Changes not staged for commit:
	  (use "git add <file>..." to update what will be committed)
	  (use "git restore <file>..." to discard changes in working directory)
			modified:   foo.txt
			
Now let's say I want to switch to an earlier branch in history. In this case it's a branch called `state`, and you can see the graph here:

	*   677e872 - (12 minutes ago) Merge branch 'dev' into master - Leo King (HEAD -> master)
	|\  
	| * e0af84b - (49 minutes ago) Change foo.txt - Leo King (dev)
	* | e576bfc - (41 minutes ago) Modify foo.txt an alternate way - Leo King
	|/  
	*   4d4655c - (23 hours ago) Merge branch 'indigobranch' into master - Leo King (state)
	|\  
	| * cef4d1c - (23 hours ago) Add indigo.txt - Leo King
	* | 3953e1e - (23 hours ago) Add violet.txt - Leo King
	|/  
	* 79f4ee2 - (23 hours ago) Add foo.txt - Leo King
	
Here's what happens when I try to switch to `state`:

	$ git checkout state
	error: Your local changes to the following files would be overwritten by checkout:
			foo.txt
	Please commit your changes or stash them before you switch branches.
	Aborting
	
Here Git is nice enough to explain the problem *and* the solution. I can't change to the `state` branch because my local work would be overwritten. Either I can add or commit my latest changes, or if I don't want to do that for some reason, I can **stash** them.

This basically means "putting away" my changes so that they're not in my working directory, but in a way that I can recover those changes later if I want to. Stash works on a **stack** - if I add something to the stash it will go to the top of the stack, and that will be the first value I retrieve when I use `git stash pop` or `git stash apply`.

So first, let's try stashing my local changes.

	$ git stash
	Saved working directory and index state WIP on master: 677e872 Merge branch 'dev' into master
	$ git stash list
	stash@{0}: WIP on master: 677e872 Merge branch 'dev' into master
	$ git checkout state
	Switched to branch 'state'
	
We can see that the stash has worked successfully - we've saved the contents of the working directory to a stash, and then we can see the results of that when we do `git stash list`. The list shows us an ID for our stash. We can use that ID if we want to revert our changes back to normal. To do so, we should switch back to our original branch where we were working, and then use:

	$ git stash apply stash@{0}
	On branch master
	Changes not staged for commit:
	  (use "git add <file>..." to update what will be committed)
	  (use "git restore <file>..." to discard changes in working directory)
			modified:   foo.txt

	no changes added to commit (use "git add" and/or "git commit -a")
	
Notice how git stash apply also includes a call to `git status`, showing us that `foo.txt` has once again been modified and needs something to be done to it. We can see this if we try to switch to `state` branch - again, it won't let us.

	$ git checkout state
	error: Your local changes to the following files would be overwritten by checkout:
			foo.txt
	Please commit your changes or stash them before you switch branches.
	Aborting
	
We could also use `git stash pop` instead of apply - this will remove the last value from the stash stack and then apply it. Also, we can use `git stash push` instead of `git stash` - the two statements are equivalent.

Now I'm going to add and commit my changes so that there are no further conflicts. Notice in gitk how there's still an item in the stash:

![[Pasted image 20210624174001.png]]

We can also see this by checking the stash list:

	$ git stash list
	stash@{0}: WIP on master: 677e872 Merge branch 'dev' into master
	
We can clear the stash using:

	$ git stash clear
	
![[Pasted image 20210624174114.png]]

That makes things neater and nicer!