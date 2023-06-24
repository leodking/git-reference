# Git - Fast-forward merge
Fast-forward merging is when you want to merge an earlier commit to a later commit, where there is a **direct path** between the two commits. Let's illustrate:

Suppose we have just one branch: `master`. Let's create another branch on it called `test` and switch to it immediately.

	$ git checkout -b test
	
Now let's create a file, then stage the change in Git and make a commit:

	$ touch foobarbaz.txt
	$ git add foobarbaz.txt
	$ git commit -m "Foo bar baz"
	
Now let's make a change to foobarbaz by adding some text in:

	$ echo "Here's some random text" >> foobarbaz.txt
	$ echo "Here's some more nice text." >> foobarbaz.txt
	
And this time we can be fancy and do the add and commit in the same line:

	$ git commit -a -m "Update foo bar baz"
	
If we check gitk, we'll see that we've made two commits on `test` branch, and are now therefore two commits ahead from `master`:

![[Pasted image 20210622165825.png]]

You can see from the graph that there is a direct path from `master` to `test`. So the merge we're going to do here is very simple: we are going to **fast-forward** the master branch, basically moving the pointer from master up to the current commit, so that master is caught up with everything we've been doing.

In order to merge test into master, we must switch into the earlier commit - in this case, `master`, and then do a git merge. This is what happens:

	$ git checkout master
	Switched to branch 'master'
	$ git merge test
	Updating f7fe5af..b8b243a
	Fast-forward
	 foobarbaz.txt | 2 ++
	 1 file changed, 2 insertions(+)
	 create mode 100644 foobarbaz.txt
	 
You can see from the log that a **fast-forward merge** has been performed. Now we can also see from gitk that this merge was successful!

![[Pasted image 20210622170209.png]]

Now that we have successfully merged `test` and `master`, we have no more need for the `test` branch. We can delete it like so:

	$ git branch -d test
	$ git branch
	* master
	
We have verified that only one branch now exists - master.

### Fast-forward merge workflow - Summary
1. Create a new branch using `git checkout -b newbranch`
2. Do work on newbranch as you see fit, then stage it and create commits.
3. Switch back to the main branch (the branch you want to merge your changes into, which should be earlier in your commit history)
4. Do `git merge newbranch` to fast-forward your main branch to your `newbranch`, making both branches in line with each other.
5. Get rid of the unneeded branch using `git branch -d newbranch` (if this doesn't work, it means that the merge hasn't worked properly.)

#git 