	git checkout --patch <tree|branch|commit>

Switch to the branch you want to make changes to. Then in the <> argument, select the branch, tree, commit etc. that you want to bring in changes from.

So say I am on branch **main** and I want to pull in changes from branch **develop**. I'll do something like this:

	git checkout main
	git checkout --patch develop

This will pull in 'hunks' of a file one at a time.