# Git - Three-way merge
A three-way merge needs to happen when you want to merge two branches that are in different places on the tree - i.e. there's no direct track between them. I'll create a new repo to illustrate (mostly because I messed up the old repo while testing this, and decided to nuke the old repo and start again.) ...

	$ git init
	Initialized empty Git repository in /home/leokin01/git/sandbox/.git/
	$ echo "foo" > "foo.txt"
	$ git add foo.txt
	$ git commit -m "Add foo.txt"
	[master (root-commit) 79f4ee2] Add foo.txt
	 1 file changed, 1 insertion(+)
	 create mode 100644 foo.txt
	 
	$ echo "Violet is the best colour." > violet.txt
	$ git branch indigobranch
	$ git add violet.txt 
	$ git commit -m "Add violet.txt"
	[master 3953e1e] Add violet.txt
	 1 file changed, 1 insertion(+)
	 create mode 100644 violet.txt
	 
	$ git checkout indigobranch
	Switched to branch 'indigobranch'
	$ git branch
	* indigobranch
	  master
	$ echo "Indigo is the best colour." > indigo.txt
	$ git add indigo.txt 
	$ git commit -m "Add indigo.txt"
	[indigobranch cef4d1c] Add indigo.txt
	 1 file changed, 1 insertion(+)
	 create mode 100644 indigo.txt

What we've done here is briefly: from the master branch, made a branch called `indigobranch`. Then we've added the `violet.txt` file and made a commit, which has moved `master` ahead of `indigobranch`. Then we've switched back to `indigobranch` and added another file, `indigo.txt`, then made a commit. This has given us two branching paths:

![[Pasted image 20210622175024.png]]

We can't do a fast-forward merge here because the two branches, `indigobranch` and `master`, don't directly link to each other. Instead the solution is to do a **three-way merge**, which will merge the previous commit (where we have the message "Add foo.txt") with the `master` commit and the `indigobranch` commit. This merge will then produce a fourth commit, joining back up the two branches.

The result is what's known as a **merge commit**. Let's try it. First we must make sure we are merging from the **parent** branch, i.e. `master`:

	$ git checkout master
	Switched to branch 'master'
	$ git merge indigobranch
	Merge made by the 'recursive' strategy.
	 indigo.txt | 1 +
	 1 file changed, 1 insertion(+)
	 create mode 100644 indigo.txt

And we can see the result from here:

![[Pasted image 20210622175950.png]]

## Three-way merge summary
1. Create a new development branch using `git checkout -b newbranch`
2. Do some work on that branch, then stage and create commits
3. Switch back to the main branch, then do some work on this branch and create a commit. Now you will have branching paths, with `master` on one end and `newbranch` on the other.
4. To create a merge commit, switch back onto `master`, then do `git merge newbranch`. 
5. A commit message will show up indicating that a Merge commit is taking place. Save the commit message using `:wq` in Vim and continue.
6. A three-way merge will be performed, combining changes from the parent, `master` and `newbranch` commits.
7. Get rid of the unneeded branch.

#git 