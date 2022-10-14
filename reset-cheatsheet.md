# git reset - cheatsheet


## Resources

- [An incredibly helpful series of animated diagrams showing file state changes for Git Reset](https://www.practiceprobs.com/problemsets/git/intermediate/#__tabbed_4_4)
- [Reset Demystified - From the Pro Git book](https://git-scm.com/book/en/v2/Git-Tools-Reset-Demystified)
- [Difference between Git reset and checkout](https://stackoverflow.com/questions/3639342/whats-the-difference-between-git-reset-and-git-checkout)
- [In Plain English, what does Git reset do?](https://stackoverflow.com/questions/2530060/in-plain-english-what-does-git-reset-do)

### A few other resources I haven't fully checked out
- [The difference between soft, mixed and hard reset](https://davidzych.com/difference-between-git-reset-soft-mixed-and-hard/)
- [What's the difference between soft, mixed and hard reset? (SO question)](https://stackoverflow.com/questions/3528245/whats-the-difference-between-git-reset-mixed-soft-and-hard)
- [How does Git Reset actually work? (Howtogeek)](https://www.howtogeek.com/devops/how-does-git-reset-actually-work-soft-hard-and-mixed-resets-explained/)
- [Why bother using --mixed reset over --soft?](https://stackoverflow.com/a/61032523/1907765)
- [Practical usage of --soft reset](https://stackoverflow.com/questions/5203535/practical-uses-of-git-reset-soft)
  - Basically, an alternative method of squashing commits to `git rebase -i HEAD~n`

| Command                      | Meaning                                                                                                      |     |
|:---------------------------- | ------------------------------------------------------------------------------------------------------------ | --- |
| `git reset --soft HEAD~1`    | Move branch pointer to the previous commit (don't update stage/working directory)                            |     |
| `git reset [--mixed] HEAD~1` | Do the same as above, but update the index to the previous commit as well (default behaviour)                |     |
| `git reset --hard HEAD~1`    | Do the same as above, and additionally update the working directory (dangerous! you can lose work this way!) |     |
| `git reset [HEAD]`           | If no arguments are specified, HEAD is assumed. Branch is moved and staging area is updated, but WD is not   |     |
| `git reset --hard HEAD`      | Reset the WD to the state of HEAD                                                                            |     |
| `git reset [file]`           | Unstage a file                                                                                                             |     |

A note about the last one: `git reset [file]` will unstage a file because it's resetting

![image](https://user-images.githubusercontent.com/72651324/189367482-21d15018-b0ca-4e61-9b95-f12b6d12a1f3.png)
Source: https://marklodato.github.io/visual-git-guide/index-en.html#reset


## Why use each version of reset?

### Soft reset

A soft reset can actually be a very useful way of combining commits into one. This is because we can use it to update the working tree to a previous commit that we've done. Then we can add and commit the contents of that commit, and this will discard the previous commit.

It's an alternative to squashing commits using `git rebase -i`
