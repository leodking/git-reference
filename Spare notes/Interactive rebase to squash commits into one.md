---
aliases: [Combine commits into one, Use soft reset to squash or combine commits]
---

Let's say I have multiple commits and I want to squash them into one. In this example:

	ccd684b (HEAD -> feature) Okay now the commit is done I'm happy with it (4)
	2b2b5e2 Then some more work after that (3)
	25db979 And just a bit more work (2)
	8b12055 Add a little bit more work (1)
	48b9ec5 Do some work
	e140385 (origin/main, origin/HEAD, main) Good commit

e140385 is the main branch, it's the good one. I want to squash ccd684b onto 48b9ec5, so that 48b has everything from ccd in it.

To do this, I type git rebase -i and select the commit **BEFORE** the one that I want to squash onto. So that's the "main" branch commit in this case.

	$ git rebase -i e140385
	
	pick 48b9ec5 Do some work
	squash 8b12055 Add a little bit more work (1)
	squash 25db979 And just a bit more work (2)
	squash 2b2b5e2 Then some more work after that (3)
	squash ccd684b Okay now the commit is done I'm happy with it (4)
	
	# Rebase e140385..ccd684b onto e140385 (5 commands)

In this output, **the oldest commit is at the top, the newest commit is at the bottom.** You can see this from the numbers in the commit messages.

So essentially I **pick** the oldest commit, and squash all of the others into that. It makes no sense, I know. But that's how we do it.

Then all of the code in the `ccd` commit will be in the `48b` commit, and it will combine the history of the commits into one single commit.

**Pick the oldest commit (the one at the top), squash the rest into it**

## ALTERNATIVE METHOD
```
git reset --soft <COMMIT I WANT TO RESET TO>
git commit -m "Commit message"
```

This is an easier way to squash commits. This will move the branch pointer to my specified commit, but not update the index or working directory

So in this case:

```
git checkout feature
git reset --soft main
git commit -m "Commit message"
```