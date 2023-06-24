Git maintains a **HEAD** variable, which is a **pointer** to the tip of the current branch in the repository. It indicates the most recent state of the repository, i.e. the latest commit. As we make new commits, the HEAD pointer moves.

The HEAD pointer is like the "record" button on an old-fashioned cassette player. We can hit play and play our tape for a bit, or fast-forward or rewind. Whatever position we're at on the tape, when we hit "record", the machine will start recording **from that position**. So the HEAD pointer is like the record feature - it tells Git where to start writing commits from, if you stage and commit any changes to your repository.

Another way to think of it is that HEAD is simply a "bookmark" for whichever **commit** and **branch** you're currently viewing in Git. E.g. let's say you have one commit on a master branch, and it's SHA-1 value abbreviates down to a5fb23:

	master
	a5fb23
	HEAD
	
The HEAD is currently pointing to this commit, which is on the master branch. If we make 2 additional commits, it will look like this:

	                      master
	a5fb23 <-- 8827bc <-- 123cf9
	                      HEAD
						  
## Detached HEAD
[[Detached HEAD and how to fix it]]

#git