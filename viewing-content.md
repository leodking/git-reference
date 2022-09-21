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

## Viewing the contents of a Git object

To view the contents of a `blob`, `tree`, or `commit` in the Git object database, just use `cat-file`:

```bash
# Use the -p option to print the object in a human-readable format
$ git cat-file -p <hash>

# E.g. if `abc1234` refers to a blob object:
$ git cat-file -p abc1234
Some file
...

# Use -t to get the type of an object
$ git cat-file -t abc1234
blob

# And use -s to get the size of an object
$ git cat-file -s abc1234
1234
```

## Viewing special branches

### All branches

```
git branch --all -vv
```

### Remote branches only

```
git branch -r
```
