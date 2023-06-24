# Detached HEAD
[[HEAD]]
## What it is
We get into a detached HEAD state whenever we switch to a previous commit back in time. This means that the HEAD is not attached to any particular branch. Let's try this. I've made some commits in a test repo, and now I'm going to switch to an earlier commit in the history to show what happens:

	$ git checkout 4d46
	Note: switching to '4d46'.

	You are in 'detached HEAD' state. You can look around, make experimental
	changes and commit them, and you can discard any commits you make in this
	state without impacting any branches by switching back to a branch.

	If you want to create a new branch to retain commits you create, you may
	do so (now or later) by using -c with the switch command. Example:

	  git switch -c <new-branch-name>

	Or undo this operation with:

	  git switch -

	Turn off this advice by setting config variable advice.detachedHead to false

	HEAD is now at 4d4655c Merge branch 'indigobranch' into master
	
We can also see this by checking git status:

	$ git status
	HEAD detached at 4d4655c
	nothing to commit, working tree clean

Or gitk in ASCII format using [[git graph - alias]]:

	$ git graph 
	*   677e872 - (15 minutes ago) Merge branch 'dev' into master - Leo King (master)
	|\  
	| * e0af84b - (52 minutes ago) Change foo.txt - Leo King (dev)
	* | e576bfc - (43 minutes ago) Modify foo.txt an alternate way - Leo King
	|/  
	*   4d4655c - (23 hours ago) Merge branch 'indigobranch' into master - Leo King (HEAD)

Or gitk in graphical format:

![[Pasted image 20210623170535.png]]

Notice that gitk and git graph don't actually tell us in words that we have a "detached HEAD" - only git status is kind enough to inform us so. In gitk we can see this through the yellow dot, and the fact that the commit doesn't have any branch attached to it.

## Solutions
There are two ways out.

1. Just switch to any other branch. Problem solved.
2. Create a new branch at your detached HEAD location and then switch to it.

Let's try option 2. First we'll create a new branch:

	$ git branch state
	
Let's see what happens:

![[Pasted image 20210623171147.png]]

It looks promising, but when we check `git status` we'll see that we're still in a detached HEAD state, so all is not fixed. `git graph` makes this more obvious:

	$ git graph
	*   677e872 - (23 minutes ago) Merge branch 'dev' into master - Leo King (master)
	|\  
	| * e0af84b - (60 minutes ago) Change foo.txt - Leo King (dev)
	* | e576bfc - (51 minutes ago) Modify foo.txt an alternate way - Leo King
	|/  
	*   4d4655c - (23 hours ago) Merge branch 'indigobranch' into master - Leo King (HEAD, state)
	
Notice that there is no arrow pointing from HEAD to state. They just happen to be in the same place, but HEAD is not pointing anywhere still. We have to use checkout or switch.

	$ git checkout state
	Switched to branch 'state'
	$ git status
	On branch state
	nothing to commit, working tree clean
	
Now see gitk:

![[Pasted image 20210623171611.png]]

See the difference from earlier?

![[Pasted image 20210623171147.png]]

It's a subtle one - `state` is not bolded in the earlier picture, which indicates that HEAD is not pointing to it. Now we have attached our HEAD to the `state` branch, and the branch is bolded accordingly. This becomes clearer when we check the graph:

	$ git graph
	*   677e872 - (28 minutes ago) Merge branch 'dev' into master - Leo King (master)
	|\  
	| * e0af84b - (65 minutes ago) Change foo.txt - Leo King (dev)
	* | e576bfc - (56 minutes ago) Modify foo.txt an alternate way - Leo King
	|/  
	*   4d4655c - (23 hours ago) Merge branch 'indigobranch' into master - Leo King (HEAD -> state)