# Git idioms

Git has a reputation for being confusing. Why use one word for something when it could use three words to refer to the same thing, after all? Here are common terms used in Git and their meanings.

## Repository / Repo

A repository is a directory (or folder) containing all of the files and sub-directories in your project. Typically code projects are stored in repositories, but you don't have to use them to store code. For example, this is a repository containing mostly Markdown files (.md).

One way to think about a repository ('repo' for short) is in comparison to tools like Google Docs, which stores separate versions of your files. At any point you can "go back" to a previous version of your document, because it's stored in the history. A repository is like this, with a crucial difference: instead of storing the difference between one file over time, it stores the differences between multiple files over time. You can still use your Git repository to switch between different versions of your file collection at any time.

Despite what I just said about repositories not only being for code, for clarity and brevity I'm going to refer to the contents of a repository as "code" or a "code-base" from here on out. It's just simpler, because that's the most common use-case of using Git for version control - to track changes in a code-base within a single repository.

## Snapshot / Commit

"Commit" is a somewhat confusing term in Git, which is usually explained by the term "snapshot" as if that clarifies everything. "A commit is a snapshot of your code at one moment in time" might be a typical definition.

What this means in practice is: a commit is a complete, independent version of all of the files in your repository at any one time. In other version control systems, your files might only be stored once, and every time you create a new "version" of your repository, that "version" will simply point back to the first version of your file if nothing has changed. This is known as "changeset-based version control", or "delta-based version control". Git is "snapshot-based version control", and this means that each time you make a commit, a new copy of your files is stored again. (Kind of. It's a little more complicated tha this in reality, but this will do for now.)

So one way you can think of a commit is like a "version". It's commonly referred to as a "snapshot" because it's like a photograph in your family photo album. If you take a family photo each year, and one year dad is wearing a green jumper, the next year mum has slightly greyer hair etc., you're still taking a photo of the whole family every time. It's not as if you'll write down on one page "Dad wore a different jumper, mum looks the same as last year." That's the difference between storing commits as "snapshots" versus "changesets"

This page from the Pro Git Book clarifies the difference between snapshots and changesets with some nice diagrams:
https://git-scm.com/book/en/v2/Getting-Started-What-is-Git%3F

## Parent / Root commit / Commit timeline

The first thing to say about a commit is, when we are discussing how Git works in an abstract way, we typically don't care what a commit actually "is". In Git tutorials, people will typically use a single letter, number or symbol to represent a commit, like this:

```
A
```

Where `A` could mean anything from this ...

```
myfolder
|- some-text-file.txt
`- README.md
```

... to the entire Linux kernel. It doesn't matter what it is, it's just a useful abstraction that helps us understand that commits exist and are separate from one another.

The second thing to say about a commit is that every commit (except the first one) has a **parent**. This means the commit that came immediately before it. Each commit contains a pointer to its parent.

For that reason, when we're talking about Git commits we typically draw a timeline which goes from left-to-right, although we often draw arrows going from right-to-left. This can seem confusing at first. In the example below, there are four commits. `A` is the first, then `B`, then `C`, then `D` last. Commit `B` has an arrow pointing left to commit `A`, which indicates that `A` is the parent of `B`.

```
A <-- B <-- C <-- D
```

In this example, all commits except for `A` have a parent. A does not have a parent, because it is the **root commit**

Remember: time moves from left-to-right, but commits always point to their parents (from right-to-left)

### Graphical view of branches / tags / references

You don't need to fully appreciate what a "branch", "tag" or "reference" is at this point. The important thing to note is that tutorials will typically show Git commits in a graphical format, going either left-to-right, or top-to-bottom. In the left-to-right example, the format will usually show a branch, tag or some other kind of reference coming off either the top or the bottom of a commit. For example:

```
A <-- B <-- C
            |
          main
```

This is a graphical representation of a Git repository with three commits. The label `main` is pointing to commit `C`, indicating that the `main` branch ends with commit C.

Because a commit can have multiple branches (or tags, or other references like `HEAD`), these labels are often stacked on top of each other, like this:

```
A <-- B <-- C
            |
          main
            |
          HEAD
```

## The three areas / The three trees / The three worlds

In Git tutorials you'll typically hear people talk about "The Three Areas". These are in a sense, three "states" that your code has to go through before it can become a "commit" (a fixed version) in your repository. These are:

1. The working directory <- The current version of your code
2. Staging area <- A version of your code that you would like to put into a commit
3. Repository <- A database containing all "commits" or versions of your code

### Working directory / Worktree / Working copy

This is another term with several confusing synonyms. Your "working directory", or "worktree", or "working copy", is the version of your code that you are currently working on. For example, if you are making a website, you might have a `website` directory with several files under it, like this:

```
website
|- index.html
|- style.css
`- script.js
```

While you're working on these files and before you've created any "commits" using Git, this is your working directory.

It's also called a "worktree" because the top-level directory can also contain many nested sub-directories. For this reason your directory can look like a "tree" in the mathematical / computer science meaning, or a data structure with many branches. Like so:

```
website
|- css-scripts
|   |- mainpage.css
|   `- style.css
|- html
|   |- landing-page
|   |   `- welcome.html
|   |- product-page
|   |   `- product.html
|   `- shopping-cart
|       `- cart.html
`- javascript
    |- shopping-scripts
    |   `- script.js
    `- other-scripts
        `- script.js
```

And so on. All of this is contained within your "worktree" or "working directory". The term "working directory" refers to all files and directories within the top-level directory (e.g. `website` in this example.)

### Index / Staging area / Cache (and what a "commit" is)

These are all terms for the exact same thing. I know, lovely and confusing. Probably the most common term you'll hear is the "staging area". To understand the staging area, you might need to understand a bit more about what a commit is.

We've already said that a commit is a "version of your repository" above. But it's not necessarily every single file and directory in your repository. When you create a new Git repository, Git will only care about the files that you tell it to care about. So if you have a directory with 1,000 files, it won't keep track of those 1,000 files until you create a commit with all of those files in it.

This is where the staging area comes in. It's an intermediate step between your working directory and a commit.

Let's say I create a repository for my website project, and add two files: `index.html`, and `style.css`. Imagine I want to create a commit with only the HTML page in it. I can do that using the commands:

```
git add index.html
```

Now what I have done is add `index.html` to the "staging area". This means that if I type `git commit`, this file and this file only will go into a commit, or a "version" of my website project, and be stored in the repository:

```
# This creates a new commit containing the file index.html
git commit
```

Let's say I want to create a commit with both files in it now. To do that, I do:

```
# Add style.css to the "staging area" and prepare a new commit
git add style.css

# Create the commit and store it on the repository
git commit
```

Summary: the purpose of the staging area is to **prepare a new commit to be stored safely in your repository**.

### Repository / Repo / Local repository

We already covered what a repository is above, but it's worth expanding on how the repository fits into this model. When you add files to the staging area using `git add`, you then create a commit which contains those files using `git commit`. Now you have a "commit", or a discrete version of your files at one point in time. You can make any changes you like to your files. In the example above, you can modify and even delete `index.html` and `style.css` from your working directory - it doesn't matter. Git has saved your files into a commit, and can easily recover them for you and insert them back into your working directory at a moment's notice.

## SHA-1 / SHA / Hash / Commit ID

"SHA-1" stands for "Secure Hash Algorithm 1". It is a "cryptographic hash function". If you don't know what this means you don't really need to: the short story is that, given an input string, it will output a string of digits in hexadecimal, which is rendered as 40 characters.

"Hexadecimal" is a representation of a number in base-16 instead of the usual base-10, which means that each digit in a number goes from 0-9, and then A-F. So for example the hexadecimal number F is 15 in decimal; 10 in hexadecimal is 16 in decimal, and so on.

Because of this, SHA-1 hashes may look like strings of random characters, e.g.:

```
0beec7b5ea3f0fdbc95d0dd47f3c5bc275da8a33
```

But importantly, they are **not random**. If you give the same input to a SHA-1 algorithm, it will give you the same output every time. This output is usually simply known as a "hash" or "SHA", which is short for "SHA-1" hash. We can test this in a Linux terminal like below:

```bash
# The following command will convert "foo" into a hash using SHA-1
$ echo -n foo | sha1sum
0beec7b5ea3f0fdbc95d0dd47f3c5bc275da8a33  -

# And it will do the same thing every single time
$ echo -n foo | sha1sum
0beec7b5ea3f0fdbc95d0dd47f3c5bc275da8a33  -

# But if we change the input string we get something completely different
$ echo -n moo | sha1sum
24a56b37819e0452df9c07432e5dd2e2b5cebf48  -
```

The point of a hashing algorithm is that (at least in theory) it's one-way. You can generate hash from a string input, but you can never reconstruct the string input from the same hash. And because of the above principle that **the same input will always generate the same hash**, Git can use hashes to easily check if anything has changed in your repository. For example, each of your files in the repository will be referenced using a SHA-1 hash. If you change the file even by one character, the hash will change too, and Git will know that you have made a change. (See the discussion about the object model for more information on this).

Note that there are other SHA algorithms, such as SHA-2, SHA-3 and SHA-256. The SHA-1 algorithm is actually considered to be "broken", meaning that a well-funded hacker could potentially break the algorithm. For that reason, Git is currently transitioning to the SHA-256 algorithm, which is much more secure (and also produces a longer hash string).

In Git terminology, you will usually hear the terms "SHA", "SHA-1", "hash", "id", and these are all referring to the same thing: the 40-character string representing a commit, blob or tree object.

## The object model / Object database / Blob, tree, commit, reference

This is an important thing to understand in Git, but it is also quite helpful. Basically, read this: https://github.blog/2020-12-17-commits-are-snapshots-not-diffs/

The essence is that Git is an **object database**. This might sound complicated, but what Git boils down to is nothing fancier than a list of key-value pairs, like an associative array (dictionary in Python, hash map, hash table and other terms in other languages).

- The "key" is a SHA hash as we have discussed in the previous section.
- The "value" is the contents that you are storing, which could be a file, a commit, or a tree (more on this shortly)

These two resources explain this very well, especially the first one:
- https://github.blog/2020-12-17-commits-are-snapshots-not-diffs/
- https://git-scm.com/book/en/v2/Git-Internals-Git-Objects

It boils down to this. In Git, there are basically three types of **object** that can be stored in the **object database**:
1. Blob - This stands for "Binary Large Object", but what it basically amounts to is a single file in your Git repository
2. Tree - This is a list of files and directories - actually it is just a list of blobs and trees.
3. Commit - This represents a "snapshot" of your code at one point in time.

It starts with **blobs**. A blob is an encrypted form of a file, which your Git repository knows about. Git doesn't know the name of your file; this is recorded using a "tree".

Then **trees** are used to store the directory structure of your project. One tree only stores one "level" of hierarchy. For example if you have a nested folder, the first tree will show every file in the top-level directory as a "blob", and every directory as another "tree" object. Then if you were to open each tree object, you would see that it, too, contains a list of blobs and trees. In this way, you can store the contents of a repository using only blobs and trees.

Lastly, **commits**. A commit represents your repository at one point in time, and so all it boils down to is a pointer to a "tree", which in turn points to all of your code files in the state they were in when you committed them. A commit also contains information about the author and committer of a commit, the date it was committed, and the commit message provided.

Each of these objects are stored in the object database using a **SHA-1** hash as the key. The value is the contents itself. For example, a "blob" (single file) will have a SHA-1 hash or ID. That ID is the "key" to access the contents of that file. You can verify this by using the `git cat-file -p` command on a blob ID to see its contents:

```bash
# Where "abc1234..." is the hash of a blob in your Git repository
$ git cat-file -p abc1234...
```

## Branch / Tag / Pointer / Reference

If you've absorbed the above section, remember that Git is an object database which consists of three types of objects: a "blob" (file) "tree" (listing of a single directory) and "commit" (pointer to a tree representing your repo at one point in time, plus metadata).

You might know that Git has "branches", and think that this must introduce some extra complicated object into Git's object model. But no, branches are surprisingly simple. A branch is just a single file containing the SHA hash of a commit. It is a "pointer", also known as a "reference". This is why branches in Git are really fast and cheap to create and destroy - they're ultimately just a single file containing 40 characters and a line return. When you make another commit on a "Branch", the branch pointer will then move to the new commit.

Tags are similar. A tag is a "fixed" name for a commit, meaning that if you run "git commit" after giving a commit a tag name, the tag will not move or change. But the underlying principle of a tag is the same: it's a pointer to a particular commit. The only difference between tags and branches is in usage - tags are used generally for fixed versions, e.g. for a major release like "v1.0.0". Branches are meant to track commits along different stages of development, so you might have something like the `main` branch (formerly called `master`), and you might create branches like `feature`, `experiment`, `bugfix`, `hotfix`, or `whatever-the-heck-I-want`.

So a reference, such as a branch or tag, ultimately is a pointer to a commit. And remember that a commit is ultimately a pointer to a tree, or the state of your repository at one point in time. And trees point to files. Putting all of that together, you could think of it like this:

```
branch/tag --> commit --> tree --> blobs
```

A very useful resource which explains the principles behind references, Git commits, and the commit graph in more detail: http://think-like-a-git.net/

## HEAD

"HEAD" can seem like a very confusing and mysterious term when you first encounter it. But if we've understood the above, then it should make a lot more sense: HEAD is just a **reference**. In particular, it's a reference to the **branch** that we're currently on. Remember that a branch points to a commit - so HEAD just points to the latest commit on our branch.

It **does not** refer to the files that we're currently working on - which are in the "working directory" or "working tree" as discussed above. It also **does not** point to the contents of the index. In terms of the "three areas" we discussed before, "HEAD" belongs to the **local repository** area, because it points to a commit that is actually checked into your local repository.

### Detached HEAD / What a branch "really is"

Another confusing and (perhaps) unhelpful term for newcomers. When you do work in Git, you typically do work on a branch, such as the `main` branch. You can use the `git checkout` or `git switch` command to move to another branch, like this:

```
# Move to 'feature' branch
$ git checkout feature

# Move back to 'main' branch
$ git checkout main
```

But you can also move to a commit that's earlier along on the same branch. To do this we can write `git checkout HEAD~1`, which means "Go back one commit from `HEAD`"

```
# Switch to the previous commit on the current branch
$ git checkout HEAD~1
Note: switching to 'HEAD~1'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false
```

And you get all of this strange advice about a "detached HEAD". All that means is that you're not currently "on a branch".

This might sound confusing. After all, isn't a branch all of the commits that led up to your current commit? Actually, no. A "branch" is just a name for a particular commit. If you make some changes to your code and make a new commit, your branch will move onto a new commit. The old commit will no longer be "on" your branch. It's **reachable** from your branch, but the commit itself does not belong to a branch.

Therefore, if you use `git checkout` or `git switch --detach` to move to a commit that doesn't have a branch pointing to it, Git will tell you that you are in a "detached HEAD" state.

There's a very easy fix for this state - just move back to a commit that's on a branch:

```
git checkout main
```

## Unmodified / Modified / Staged / Committed
