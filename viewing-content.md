# Ways to view content in Git:

## Show the contents of the index:
```bash
$ git ls-files
```

Use `git ls-files -s` to show the blob as well

## Show the contents of the current commit (at HEAD)

```bash
$ git ls-tree <branch>

# e.g.
$ git ls-tree main
$ git ls-tree HEAD
$ git ls-tree 123abcd
```

You can also use `git ls-tree <commitish> --name-only` to see the names only of a particular commit.

## How to view the SHA hash of any ref

A "ref" or "reference" means a branch, a commit, a tag, or anything which points in some way to a commit. Every commit has a unique SHA-1 ID, which is a hash of the contents of the commit, as well as metadata like the author and committer.

For example, if you're on branch `main`, you can get the hash of that using the `git rev-parse` command:

```bash
$ git rev-parse main
abc1234abc1234...
```
https://stackoverflow.com/a/28249368/1907765
