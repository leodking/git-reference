**git status** - To view the branch, commits and untracked files in a project. All files in a git repo are untracked by default. Only track source files, omit anything that can be generated from those files

	$ git status
	On branch master

	No commits yet

	Untracked files:
	  (use "git add <file>..." to include in what will be committed)
			index.html
			
Use this to ignore untracked files:

	$ git status -uno
	On branch master
	nothing to commit (use -u to show untracked files)
	
#git