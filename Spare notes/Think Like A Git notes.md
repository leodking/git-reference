- Graph theory, e.g. Euler's solution to the Seven Bridges of Konigsberg problem, basically boils down to: **Places to go, and ways to get there**
- A node in a graph is a "place to go". An edge in a graph is a "way to get there"
- We can attach labels to nodes (as in stations on London's Underground map), and we can attach labels to edges (e.g. to express relationships or direction between nodes, names of roads, numbers/weights)
- Graphs can be **directed** (one-way, unidirectional) or **undirected** (two-way, bidirectional)
- Git commit histories basically boil down to a **directed graph**, with arrows pointing at commits which are "earlier in time", otherwise known as parent commits:

![[Pasted image 20211008104523.png]]

- Some parts of this graph will always be unreachable to you. I.e. depending on where you start, you can access some nodes and not others.
- In Git, the atomic unit is a **commit**. A commit is represented as a single node in a graph of a git repository.
- A "commit" is basically two things:
	1. A pointer to the state of your code at a moment in time, and
	2. Zero or more pointers to a parent commit.
- **References** are pointers to commits. They can take three forms:
	- Local branch
	- Remote branch
	- Tag
- A local branch reference is simply a pointer to a particular commit, stored in .git/refs/heads. That's why branching is cheap in your local repository - it's just moving a pointer from A to B.
	- Commands that affect local branch references include: commit, merge, rebase, reset
- Remote branch references are pointers to a commit stored in the remote.
	- Commands that affect remote branch references: fetch and push.
- Tag references are references to a single commit which never change. The command that affects this is: tag.
- Git periodically runs garbage collection. Some commits you make are not reachable - for example if you run `git commit --amend`, this actually creates a new commit based on your previous commit, but hides the old one from you. Because you can't easily reach this old commit, it will be removed eventually, or by `git gc`.
- The point is that **References make commits reachable**
	- References - to a local branch, remote branch or tag
	- Commits - A node in a graph
	- Reachable - Meaning you can access it through the graph.
- This means that creating a branch is really just an easy way of telling Git to "save" code that you want to come back to later. It takes more time to type `git branch foo` than it does for Git to execute the action.
- You can do this to experimentally create branches when trying something you're not sure about - e.g. a `merge` or `rebase`. This is saving the game before you go to fight the boss, in other words.
- Use your Git visualiser as often as possible in order to understand what's going on.

NB: To understand Git, you need to understand the idea of version control <-- the idea of versions <- what program code is/used for <- a bit about how computers work.