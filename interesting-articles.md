  # Interesting articles about Git

  ## Interesting articles on version control systems

- [Is Git the be all and end all of VCS?](https://dev.to/ben/is-git-the-be-all-and-end-all-of-version-control-4lp)
	- Some interesting comments, e.g. [this one](https://dev.to/jillesvangurp/comment/12dn) points out that Git struggles in large codebases, and instances where you don't need the whole repository, just a portion of it.
		- Where you could e.g. check out one single file and upload it back. That would be an interesting change.
		- Also, Git isn't "sharded", which means separating a database into smaller, manageable parts. This can apparently ease complexity.
		- Also you can't actually version control manage things like Microsoft Word files or anything in rich text - it can only be plain text. This hearks back to UNIX days, but today might be considered a limitation. Surely a flexible system should be able to version control things besides plain text.
	- And [this comment](https://dev.to/jballanc/comment/12af) which points out that Git is based on being fully distributed with more than one single source of truth, but most teams don't work that way and that it introduces unnecessary complexity.
- https://arstechnica.com/information-technology/2017/05/90-of-windows-devs-now-using-git-creating-1760-windows-builds-per-day/ <- An article about how Microsoft transitioned to Git, and the problems they found in it
	- They had to make a customised version of Git for several reasons. Apparently Git creates files unnecessarily which slows down work and causes git status to take ages.
	- They changed it so that their modified Git only cared about locally stored files which had been modified.
- The competition - https://chambers.io/2018/04/17/git-vs-the-competition.html
	- Mercurial is good and sleek but slow
	- Perforce is old and works but paid
- https://www.quora.com/Why-isnt-a-simpler-tool-than-Git-popular-for-version-control-especially-for-small-projects - Question on why there isn't a simpler tool than Git available
- [An article about the "limbo" state in Git](https://blogs.gnome.org/newren/2007/12/08/limbo-why-users-are-more-error-prone-with-git-than-other-vcses/) and why it's pernicious.
- "[A principled approach to version control](https://www.andres-loeh.de/fase2007.pdf)"- Loh et al. Interesting looking paper on algebraic approaches to version control
-  [Article from Joel Spolsky](https://www.joelonsoftware.com/2010/03/17/distributed-version-control-is-here-to-stay-baby/) on why DVCS is great
	- [Similar interesting article](https://www.joelonsoftware.com/2001/12/11/back-to-basics/) about how strings work
	- And one about the [Law of Leaky Abstractions](https://www.joelonsoftware.com/2002/11/11/the-law-of-leaky-abstractions/)

- Content addressable storage (CAS) in Git - i.e. Git uses a cryptographic key-value-based object store to store all content. It's not file-address-based, all objects are converted into hashes and compared to one another for simplicity.
	- [What are the benefits of CAS](https://stackoverflow.com/questions/65199783/what-are-the-benefits-of-content-based-addressing-in-git)

**High level problems with Git**
- Greg Szorc's [insightful article on the subject](https://gregoryszorc.com/blog/2017/12/11/high-level-problems-with-git-and-how-to-fix-them/)
- Greg Szorc's [article on Git vs. Mercurial](https://gregoryszorc.com/blog/2013/05/12/thoughts-on-mercurial-(and-git)/)
- [Paper by Perez De Rosso and Jackson](https://spderosso.github.io/onward13.pdf) about what's wrong with Git on a high level
	- [Paper by the same authors](https://spderosso.github.io/oopsla16.pdf) about redesigning Git (they created **Gitless**, which is a wrapper on top of Git which eliminates some confusing concepts)
