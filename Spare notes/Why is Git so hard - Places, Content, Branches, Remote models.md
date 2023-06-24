http://merrigrove.blogspot.com/2014/02/why-heck-is-git-so-hard-places-model-ok.html

This article talks about the **four models** of how Git works:

- The Places Model
- The Content Model
- The Branch Model
- The Remote Model

## Places Model
- There are 5 "places" in Git: stash, working directory, index (staging area), local repository, remote repository
- WD, index, local and remote are commonly used. Stash is optional. Remote repo is also optional if we are only working locally and do not need to collaborate

## Content Model
- The underlying knowledge of "objects" in Git, which include commits, blobs, hashes, refs, SHA, trees, tags, branches etc.

## Branch Model
- Following on from content model - commits 'descend' from other commits and can branch out, in a **directed acyclic graph** (DAG)
- https://git-scm.com/book/en/v2/Git-Internals-Git-Objects

## Remote Model
- Concerned with tracking branches, remote refs, remote repos.
- This is the realm of opinion and best practice - e.g. merge vs rebase, private/public branches, and team collaboration.
- Also differs with what you use to host the remote - Gerrit, GitHub etc.

Remember that Git commits are fundamentally a list of differences between the current commit and the original.

# See also
- http://think-like-a-git.net/sections/experimenting-with-git/references-make-commits-reachable.html
- https://git-scm.com/book/en/v2/Git-Internals-Git-Objects
- Git SCM in general
- Think like a git
- Git cheatsheets online