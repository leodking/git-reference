Use a combination of **git checkout** and **git branch** to switch to a new branch. It can be done in two ways:

	$ git branch newbranch
	$ git checkout newbranch
	
Or in one:

	$ git checkout -b newbranch
	
Leading to the result:

	Switched to a new branch 'newbranch'
	
So we have created and switched to a new branch. This is what shows up in gitk:

![[Pasted image 20210610171928.png]]

Notice that there are two branches attached to the current commit - "master" and "newbranch". But "newbranch" is in **bold**, indicating that it is the current branch. You can see this by typing git branch, where the asterisk indicates the current branch of development:

	$ git branch
	  master
	* newbranch
	
Let's add some new content, "hamlet.txt", to our repository, then stage it:

	git add hamlet.txt

See how it changes gitk? (You can also see a similar story from git status). Note that gitk doesn't reflect untracked files in the commit history - only tracked and staged files.

![[Pasted image 20210610172313.png]]

Now let's commit:

	$ git commit -m "To add or not to add Hamlet, that is the commit"
	[newbranch 3c1af88] To add or not to add Hamlet, that is the commit
	 1 file changed, 3 insertions(+)
	 create mode 100644 hamlet.txt
	 
And now we see that "newbranch" has moved onto a subsequent commit. While "master" is behind on the previous commit.

![[Pasted image 20210610172642.png]]

If we add another file and check it in, we can see it in gitk indicated by a green dot again:

![[Pasted image 20210610172917.png]]

	$ git add meaningoflife.txt 
	$ git commit -m "Add the meaning of life"
	[newbranch c79bf3b] Add the meaning of life
	 1 file changed, 1 insertion(+)
	 create mode 100644 meaningoflife.txt
	 
Now when we commit again, we've moved newbranch further away from master:

![[Pasted image 20210610174216.png]]

Let's say now I make a modification to "meaningoflife.txt", which is a tracked file. Notice below how the dot shows red. This means that the file is neither staged nor committed.

![[Pasted image 20210610174333.png]]

If we use git add to stage the changes, the dot turns from red to green:

![[Pasted image 20210610174628.png]]

And lastly, we can amend our commit rather than creating a new one entirely:

	$ git commit --amend
	[newbranch 163ffd8] Add the meaning of life
	 Date: Thu Jun 10 17:29:37 2021 +0100
	 1 file changed, 1 insertion(+)
	 create mode 100644 meaningoflife.txt
	 
This brings us back to our earlier picture - note that we haven't moved onto a new commit here - we simply modified the old one:

![[Pasted image 20210610174216.png]]

Now what if we switch branch back to "master"?

	$ git checkout master

This happens - notice how the yellow dot has moved to master, and **master** is now in bold, indicating this is our current branch and commit. We can see the same using git branch and git status - both will tell us we are on branch master.

![[Pasted image 20210610174849.png]]

## Splitting off and merging

Now let's say we switch to the master branch, and then we add in a new file "red.html":

	$ git checkout master
	$ git add "red.html"
	
We get this result:

![[Pasted image 20210615164459.png]]

We have split off into a new branch. Let's commit it:

	$ git commit -m "Add red.html"
	
Then this happens:

![[Pasted image 20210615164604.png]]

Lastly, let's merge the branch and see what happens:

	$ git merge newbranch
	Merge made by the 'recursive' strategy.
	 hamlet.txt        | 3 +++
	 meaningoflife.txt | 1 +
	 2 files changed, 4 insertions(+)
	 create mode 100644 hamlet.txt
	 create mode 100644 meaningoflife.txt
	 
 Then we get this result:
 
 ![[Pasted image 20210615164930.png]]
 
 Yeah I don't really understand what's going on here. I need to understand how merging works.

Then we'll tidy up by deleting the newbranch branch:

	$ git branch -d newbranch
	Deleted branch newbranch (was 163ffd8).
	
As you can see, it doesn't change much ... it just gets rid of the branch label.

![[Pasted image 20210615165149.png]]

#git