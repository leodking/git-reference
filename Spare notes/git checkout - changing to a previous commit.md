Use **git checkout** to change to a previous commit, using the first 7 characters of a hash. E.g.

    $ git log --oneline
	9a3c961 (HEAD -> master) Add blue.html
	7e7a79d Add foo.txt and orange.html
	6357c8d First commit - Create index page

You can see in gitk below that we're in a "detached HEAD" state as a result of this:
	
![[Pasted image 20210610165126.png]]

Also, the working directory has changed as a result. "blue.html" no longer exists:

![[Pasted image 20210610165256.png]]

	$ git status
	HEAD detached at 7e7a79d
	nothing to commit, working tree clean
	
We can go back further:

	$ git checkout 6357c8d
	Previous HEAD position was 7e7a79d Add foo.txt and orange.html
	HEAD is now at 6357c8d First commit - Create index page
	
Which leads to this gitk output:
![[Pasted image 20210610165515.png]]

Now how do we get back to normal? Simply this:

	$ git checkout master
	Previous HEAD position was 6357c8d First commit - Create index page
	Switched to branch 'master'
	
Leading to this output:

![[Pasted image 20210610165649.png]]

#git