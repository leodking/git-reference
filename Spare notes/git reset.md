---
aliases: [Git reset cheatsheet]
---

**Created:** 2021-09-14
**Source:** [[Git]]
**Tags:**

A great StackOverflow answer about reset:
https://stackoverflow.com/a/2530073/1907765

A nice visualisation of Git reset:
https://stackoverflow.com/a/3528483/1907765

## Basics
| Command                      | Meaning                                                                                                      |     |
|:---------------------------- | ------------------------------------------------------------------------------------------------------------ | --- |
| `git reset --soft HEAD~1`    | Move branch pointer to the previous commit (don't update stage/working directory)                            |     |
| `git reset [--mixed] HEAD~1` | Do the same as above, but update the index to the previous commit as well (default behaviour)                |     |
| `git reset --hard HEAD~1`    | Do the same as above, and additionally update the working directory (dangerous! you can lose work this way!) |     |
| `git reset [HEAD]`           | If no arguments are specified, HEAD is assumed. Branch is moved and staging area is updated, but WD is not   |     |
| `git reset --hard HEAD`      | Reset the WD to the state of HEAD                                                                            |     |
| `git reset [file]`           | Unstage a file                                                                                                             |     |

A note about the last one: `git reset [file]` will unstage a file because it's resetting 
## Visualisations
![[Pasted image 20220802132156.png]]
Source: https://marklodato.github.io/visual-git-guide/index-en.html#reset
![[Pasted image 20220405095221.png]]

Git has "three trees" that we need to understand when dealing with 'git reset'

[[The Three Trees]]

1. HEAD - a pointer to the last (most recent) commit
2. Index / Staging area - the proposed next commit
3. Working directory - our file system

Your working directory is essentially a sandbox to play around in before adding them to your staging area, and then committing them to history.

Git reset tries to do three things, in order:

1. Move the HEAD pointer to the commit that you ask it to.
2. Update your index to look the same as the commit that you point to
3. Update / overwrite your working directory to look the same as the commit you point to.

These three options correspond to:

1. git reset --soft HEAD~
2. git reset [--mixed] HEAD~
3. git reset --hard HEAD~

If you do a soft reset, it will only do the first step. That means that it will update your HEAD to the commit you specify.

![[HEAD notation]]