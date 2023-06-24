## HEAD notation
Remember that HEAD is a shorthand for the most recent commit on the current branch. We can inspect HEAD using:

	$ git cat-file -p HEAD
	
In my case it gave this output:

	tree 16283d5064f386528c1984fdac8cff3918a9b2af
	parent 0c89c3e774fcd8ddc3779bafbda6850f26718638
	author leokin01 <leo.king@emailserver.com> 1632413784 +0100
	committer leokin01 <leo.king@emailserver.com> 1632413784 +0100

	This is a new commit

The last line is the commit message of the most recent commit.


`HEAD~1` means "go back 1 commit from HEAD, using the first parent".
`HEAD~` is a shortening of `HEAD~1`.
`HEAD` means HEAD, with no going back.
`HEAD^2` means the second parent of HEAD, in a situation where HEAD has more than one parent (useful for merges only)

A useful discussion on the difference between tilde ~ and caret ^: http://www.paulboxley.com/blog/2011/06/git-caret-and-tilde

![[Pasted image 20210914181920.png]]