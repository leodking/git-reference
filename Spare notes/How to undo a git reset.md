---
aliases: [undo git reset, reflog]
---

https://stackoverflow.com/questions/2510276/how-do-i-undo-git-reset

Use git reflog to see recent changes:

```
git reflog
```

E.g.
![[Pasted image 20220912154821.png]]

Then reset back to the state you wanted using

```
git reset 'HEAD@{1}'
```

Or replace the number with the id **after** the state you want to reset back to