Git has a **three tree** model. A "tree" refers to the tree of a file or folder structure.

1. Repository
2. Staging index
3. Working copy

The repository is the stored version of a code base.

The working copy is the local version you have on your system, where you make changes to code and then push it to the repository.

The staging index exists in between the repository and the working copy.

To move between the trees, we do:

- **git add** -> to move from working directory to staging index
- **git commit** -> to move from staging index to repository
- **git pull** -> to move from the repository to the working directory

#git 