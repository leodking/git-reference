# Ways to view content in Git:

## Show the contents of the index:
```
git ls-files
```

Use `git ls-files -s` to show the blob as well

## Show the contents of the current commit (at HEAD)

```
git ls-tree <branch>

# e.g.
git ls-tree main
git ls-tree HEAD
git ls-tree 123abcd
```

You can also use `git ls-tree <commitish> --name-only` to see the names only of a particular commit.
