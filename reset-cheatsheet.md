# git reset - cheatsheet

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