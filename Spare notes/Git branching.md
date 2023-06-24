We use this to create a branch `newbranch`

	git branch newbranch
	
Then we use git checkout to switch to a branch. Let's say we're switching from `main` to `newbranch`

	git checkout newbranch
	
Let's say we do some development on `newbranch`, so we add `file1.txt`, and then do:

	git add file1.txt
	git commit -m "Add file1.txt"
	
Now let's switch back to main:

	git checkout main
	
In this case, file1.txt will **disappear** from the working directory. That's because it belongs to the newbranch branch, but not the main branch.

#git