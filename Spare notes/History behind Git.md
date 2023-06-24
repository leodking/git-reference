**Created:** 2021-09-08
**Source:** [[Git Essential Training - The Basics]]
**Tags:**

The first version control system was **Source Code Control System** (SCCS), developed for Unix in 1972, which stored the original version of the documents plus their changes. It was Unix only, developed by AT&T.

**Revision Control System** (RCS) (1982) was open-source, faster and cross-platform. It kept the **latest** version and then sets of changes. This was the difference between RCS and SCSS.

SCSS and RCS only allowed you to work with one file at a time.

**Concurrent Version Systems** (CVS) allows you to work with multiple files and an entire project. This was the precursor to:

**Apache Subversion** (SVN) - (2000). Faster than CVS, and allowed tracking of text and images. It tracked file changes collectively, and took a snapshot of the **directory**, not the **file**. This is a difference from CVS, where you considered the "latest version of a file". In SVN, you consider the file as part of the latest version of a directory. SVN was better at tracking moving/renaming files etc., because it tracks the directory as a whole, and would allow you to change multiple files at once.

**Bitkeeper SCM** (2000) Closed-source SCM. It was one of the first **Distributed Version Control** systems. The community version was free, used for Linux open-source kernel from 2002-2005. This was controversial, and Bitkeeper became no-longer free in 2005.

**Git** was created by Linus Torvalds in response to this, in 2005. Git is:
- Distributed version control
- Open source
- Free software

**GitHub** launched in 2008 to host Git repositories. By 2009, there were 50,000 repositories - by 2010, 2 million repos and 1 million users. In 2018, GitHub was purchased by Microsoft. As of 2019, there were 57 million repos and 28 million users.