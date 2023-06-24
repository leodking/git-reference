- git add --all / git add -A
	- Add everything to the index (new, modified, deleted files)
- git add --update / git add -u
	- Add modified and deleted files, but not new ones (update)
	- This has the practical effect of ignoring "Untracked" files
- git add .
	- Add everything to the index (new, modified, deleted files) **in the current folder**

Historically `git add .` used to ignore deleted files, but this is not the case anymore. Difference between `git add .` and `git add -A` is that --all will apply to files in every folder. But `.` is a **pathspec**, meaning it applies to the current directory, also called `.`. If you say `git add <pathspec>`, you mean "Stage everything in the current directory"