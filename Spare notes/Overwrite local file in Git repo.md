To overwrite one file in your local repo from the remote or another branch:

	git fetch
	git checkout origin/master <filepath>

To overwrite all changed files

	git fetch
	git reset --hard origin/master

https://stackoverflow.com/questions/3949804/force-overwrite-of-local-file-with-whats-in-origin-repo