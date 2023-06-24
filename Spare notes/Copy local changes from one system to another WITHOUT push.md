https://stackoverflow.com/questions/31854476/how-to-copy-local-changes-from-one-pc-to-another-using-git

Stash your changes with:

```
git stash save myWork
```

Save stash to file with:

```
git stash show -p  > myWork.txt
```

Move generated file (myWork.txt) to other PC Patch new PC with:

```
git apply myWork.txt
```

Clear all Stash:

```
git stash clear
```