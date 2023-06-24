https://stackoverflow.com/a/15733096/1907765

Basically, there are three local copies of your code: the local repository, the "remote" repository which is another local repository mirroring your remote repository, and your rough working copy.

- `git fetch` syncs the "remote" repository, bringing your local copy of that remote repository up to date.
- `git pull` syncs your remote repository with your local working copy - and it does this by doing a `git fetch` then usually a `git merge` into your working copy.