Say I've accidentally deleted a file in Git. It's showing up on git status like this:

	$ git status
	On branch main
	Your branch is ahead of 'origin/main' by 1 commit.
	  (use "git push" to publish your local commits)

	Changes not staged for commit:
	  (use "git add/rm <file>..." to update what will be committed)
	  (use "git restore <file>..." to discard changes in working directory)
			modified:   bar
			deleted:    foo
			
I don't want to have the `foo` file deleted. To solve that problem I simply do:

	git checkout -- foo
	
This will restore the specific file, and leave everything else untouched.

Alternatively I can do

	git checkout -- .

Which will checkout everything. I'm not sure whether that will overwrite your working directory though.

If I've staged or committed then that's a different story.