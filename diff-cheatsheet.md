# Git diff cheatsheet

| Command                        | Equivalent form                | Effect                                                                               |
| ------------------------------ | ------------------------------ | ------------------------------------------------------------------------------------ |
| `git diff`                     | `git diff <INDEX> <WORKTREE>`  | Show what changes I've made since you last staged anything (using `git add`)         |
| `git diff <commit>`            | `git diff <commit> <WORKTREE`> | Show the difference between my working directory and a commit                        |
| `git diff HEAD`                | `git diff HEAD WORKTREE`       | Show the difference between working directory and current commit (as above)          |
| `git diff --cached`            | `git diff HEAD <INDEX>`        | Show what changes will go into the next commit                                       |
| `git diff --cached <commit>`   | `git diff <commit> INDEX`      | Show the difference between what's currently staged and a given commit (less useful) |
| `git diff <commit1> <commit2>` | `git diff <commit1> <commit2>` | Show what's changed from commit1 to commit2                                          |
| `git diff <commit1> <commit2> -- <file>` | `git diff <commit1> <commit2>  -- <file>` | Show the difference between one file on multiple branches. May need to be a full path  |

Imagine that `git diff` always has 2 arguments, the `<OLD>` and `<NEW>`. When you do `git diff <OLD> <NEW>`, you are asking "What has changed in `<NEW>`?", or what files/content has been added, deleted or modified in `<NEW>`

If you specify less than 2 arguments to `git diff`, then by default the `WORKTREE`, or the working directory, is used as the `<NEW>` argument. This is because in the most common use case of `git diff`, the thing you want to know is "What changes did I make in my local working copy?"

So:

`git diff` without arguments will compare the index and the working directory - or in other words, what changes you've made locally *before* staging them using `git add`

`git diff --cached` or `git diff --staged` shows the difference between `HEAD` and the `index` - this is useful because it tells you what changes will go into the next commit when you run `git commit`.

`git diff HEAD` shows the difference between HEAD and the working directory, which lets you find out how your working copy is different from the most recent commit.

`git diff <commit1> <commit2>` tells you the difference between two commits. This can be two branches as well as commits, because branches are just pointers to commits.
