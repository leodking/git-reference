`git branch` is used to create a new branch, or view the existing branches.

Create a new branch like so:

	$ git branch newbranch
	
Check the list of **local** branches like so, e.g.

	$ git branch
	  bugfix
	  feature
	* master
	  
The asterisk shows you which branch you're currently on.

Check the list of **remote** branches like so:

	$ git branch -r
	  origin/HEAD -> origin/master
	  origin/master

#git #incomplete 