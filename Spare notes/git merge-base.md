Finds the common ancestor of two commits. For example, take the following commit graph:

	* be6054b
	* dd2e970
	* 3a3caf7
	* 522ad33
	| * 774693f
	| * 9837852
	| * dc4c759
	| * 0e6587b
	|/  
	* 2ea5e82
	* eaa2a64
	* 9ff285d
	* a1efdda
	* aa5e653

We can run `git merge-base` to discover the common ancestor of be6054b and 774693f like this:

	git merge-base be6054b 774693f

It will return the result:

	2ea5e823f8327604f8fdb395103b57921a27e3cd

This is the hash of the first commit that links to both commits.

We can usually see this with our eyes for a git graph, but it's a helpful plumbing command, and is used in git rebase.