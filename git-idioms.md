# Git idioms

Git has a reputation for being confusing. Why use one word for something when it could use three words to refer to the same thing, after all? Here are common terms used in Git and their meanings.

## Repository / Repo

A repository is a directory (or folder) containing all of the files and sub-directories in your project. Typically code projects are stored in repositories, but you don't have to use them to store code. For example, this is a repository containing mostly Markdown files (.md).

One way to think about a repository ('repo' for short) is in comparison to tools like Google Docs, which stores separate versions of your files. At any point you can "go back" to a previous version of your document, because it's stored in the history. A repository is like this, with a crucial difference: instead of storing the difference between one file over time, it stores the differences between multiple files over time. You can still use your Git repository to switch between different versions of your file collection at any time.

Despite what I just said about repositories not only being for code, for clarity and brevity I'm going to refer to the contents of a repository as "code" or a "code-base" from here on out. It's just simpler, because that's the most common use-case of using Git for version control - to track changes in a code-base within a single repository.

## Snapshot / Commit

"Commit" is a somewhat confusing term in Git, which is usually explained by the term "snapshot" as if that clarifies everything. "A commit is a snapshot of your code at one moment in time" might be a typical definition.

What this means in practice is: a commit is a complete, independent version of all of the files in your repository at any one time. In other version control systems, your files might only be stored once, and every time you create a new "version" of your repository, that "version" will simply point back to the first version of your file if nothing has changed. In Git however, each time you make a commit, a new copy of your files is stored again. (Kind of. It's a little more complicated tha this in reality, but this will do for now.)

So one way you can think of a commit is like a "version". It's commonly referred to as a "snapshot" because it's like a photograph in your family photo album. If you take a family photo each year, and one year dad is wearing a green jumper, the next year mum has slightly greyer hair etc., you're still taking a photo of the whole family every time. It's not as if you'll write down on one page "Dad wore a different jumper, mum looks the same as last year." That's the difference between the way Git stores commits, using "snapshots", compared to the way other version control systems handle commits (as "changesets")

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

### Branches / Tags / References

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

## HEAD

The HEAD is a pointer for the latest commit in a repository.

## Branch / Pointer / Reference

## Unmodified / Modified / Staged / Committed
