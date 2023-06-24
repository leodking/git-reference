See also: [[Why is Git so hard - Places, Content, Branches, Remote models|The places model]]

In Git, files can be either "untracked" or "tracked".

**Untracked** means that the file is new and is not governed by Git's version control. Git does *know* about the existence of the file - you can see it in the `git status` output under `Untracked files:`, but it doesn't *care*. The file doesn't belong to your staging area and it isn't a commit, so it isn't part of Git just yet.

**Tracked** files, on the other hand, are files which Git **cares** about somehow. They can be in at least one of three states:
- **Staged** - Means that the file has been added to the staging area (also known confusingly as the "index" or even "cache").
- **Modified** - Means that the file has been edited since being added to the staging area, **or** a file that has already been committed has been edited
- **Unmodified** - Means that a file has been added to a commit, and has not been changed since then. This state is also called **committed**, because it effectively refers to a file that can be committed.

It is possible for a file to be both **modified** and **staged** at the same time. If you create a file, then add it using `git add`, it will be **staged**. If you subsequently edit the file, it will be both **modified** and **staged** at the same time. Then if you use `git add` to add the file again, it will once again go back to **staged**. (This is captured in the diagram below)

`git status` will tell you what state a file is in - kind of. It will show you all **untracked** files under the heading `Untracked files:`. It will show you all files which are **staged** (meaning "not yet committed") under `Changes to be committed:`. It will also show you files that have been **modified** (whether or not they were modified after being added to the staging area, or after being committed) as `Changes not staged for commmit:`.

What `git status` *doesn't* tell you is about files that are **unmodified**. It is possible to find out which files are stored within a commit using several methods, such as `git log --raw` to show you file changes from each commit, or `git show --stat` to show you a summary of file changes from the latest commit. However this isn't something you'd need to do as often, so it isn't shown in the `git status` output.

The easiest way to show all of these states is to start a new Git repository and play around with them. Create files, add them, edit them, commit them and see which stage they're at after every action by reading the `git status` output.

## Cheatsheet
| Tracked?  | Stage                  | Meaning                                                                                                | `git status` output              |
| --------- | ---------------------- | ------------------------------------------------------------------------------------------------------ | -------------------------------- |
| Untracked | Untracked              | Git is aware of the file but it has not been staged or committed - it is **not** under version control | `Untracked files:`               |
| Tracked   | Staged                 | The file has been added to the staging area using `git add`                                            | `Changes to be committed:`       |
| Tracked   | Modified               | A file already tracked by Git has been modified, but not added to the staging area                                                        | `Changes not staged for commit:` |
| Tracked   | Unmodified / Committed | The file is in the commit but hasn't changed since the last commit                                     | Not indicated on `git status`                                 |
 
### When you do `git init`
- When you start a repository and start creating files, all files are **untracked**.
- Then when you add them using `git add`, they become **tracked -> staged**.
	- If you commit them using `git commit` they become **tracked -> unmodified** as they were unmodified since the most recent commit. You can also call this **committed**
	- Alternatively, if you modify the file again at this point, the file will be both **staged** and **modified**

### When you do `git clone`
- When you first clone a repository, you are starting with a commit. That means all files are currently **unmodified**
- If you modify a file in the current commit, it becomes **modified** 
- If you then add that file using `git add` it becomes **staged**
- Then if you do `git commit`, the file will become **unmodified** again
- Any subsequent new files you create will be **untracked**, then they become **staged** when you add them to the staging area, and **unmodified** when you commit them

### Summary diagram
![[Pasted image 20221014132353.png]]

### Short status cheatsheet
Note: I am using square brackets to show the position of the letters in the `git status --short` output: the real output does not show these square brackets.
- `[??]` - New file that is not tracked
- `[A ]` - New file added to the staging area (**staged**)
- `[ M]` - A file from the last commit was **modified** but not added to the staging area
- `[M ]` - A file from the last commit was modified and has been added to the staging area - it is now **staged**
- `[MM]` - A file from the last commit is both **staged** and **modified** (it has been added to the staging area, then been subsequently modified)

Some other flags are possible, but it is not necessary to specify every combination:
- `R` - File has been renamed
- `D` - File has been deleted
- `U` - File has been updated but is not merged
- `T` - File type has changed
- `C` - File has been copied