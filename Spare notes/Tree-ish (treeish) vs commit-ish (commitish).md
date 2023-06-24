A **commit-ish** is any reference object that ultimately leads to a commit. For example, a "tag" is commit-ish because it points to a commit.

A **tree-ish** is a reference which leads to a tree. For example, a tag leads to a commit, and a commit leads to a project root directory (the tree object which contains all of the code files in the project).

Commit objects always point to a tree, therefore **anything commitish is also treeish**. But not all treeish references are commitish.