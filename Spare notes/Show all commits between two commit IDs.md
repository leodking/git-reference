---
aliases: [Use git log to show all commits between two branches, refs, hashes, SHAs or commits]
---

E.g.

```bash
git log abc1234..HEAD
git log dedbeef..b33fded
git log main..branch-further-than-main
```

You can also show commits that affect a particular file like so:

```bash
git log abc1234..HEAD -- myfile
```

Show the actual files touched using --raw:

```bash
git log --raw abc1234..HEAD
```

And make the output more readable using --oneline:

```bash
$ git log --oneline --raw 57241a8..HEAD -- script.py          
56625f9 (HEAD -> feature) Some fix for script.py
:100644 100644 2b5aecf 8167af6 M        script.py
0f5a1bc Do yet even more work
:100644 100644 06c64d3 2b5aecf M        script.py
b79f27e Do some more work
:100644 100644 ecf80dd 06c64d3 M        script.py
f052873 Do some work
:100644 100644 8d36b7f ecf80dd M        script.py
4ae4295 First commit message
:100644 100644 367efd8 8d36b7f M        script.py
```