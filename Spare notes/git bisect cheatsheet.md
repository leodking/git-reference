You use git bisect to find the last "good" commit, and from there search until you find the commit that introduced your changes.

Start using:

```git
git bisect start
```

Then identify the bad commit, which is usually "HEAD" or the commit you're on:

```git
git bisect bad HEAD
```

Then specify the last known "good" commit, which could be a tag, a particular hash, or something else:

```git
git bisect good HEAD~5

<OR>

git bisect good abc1234

<OR>

git bisect good v1.2.3
```

Then the program will automatically check out a particular commit for you. Do some tests and determine if that commit is "good" or "bad". Once you've checked, type **one** of the following to tell git bisect what to do next:

```
git bisect <good|bad>
```

Then bisect will check out the next commit for you, using a binary search.

**NOTE:** If you want to stop doing bisect, type:

```git
git bisect reset
```

**ANOTHER NOTE** - If when you start the bisect you're not sure which commit to mark as the "good" commit, you can always check it out first, and then mark it as the "good" one:

```git
git checkout <experimental-commit>
git bisect good HEAD
```