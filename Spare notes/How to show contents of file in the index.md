To show a file in the index (staged but not yet committed, do)

	git show :file

You can also use `ls-files` to view the contents of the staging area. Pass the `-s` option to get the blob. Use `awk` to get the blob content, and pass to `git cat-file -p`:

https://stackoverflow.com/a/5153265/1907765

```bash
git cat-file blob $(git ls-files -s file | awk '{print $2}')
```