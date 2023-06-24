Gitk is a graphical browser used to support visualising git's project history. Here's what a normal git repository looks like in gitk:

![[Pasted image 20210610171135.png]]

- The upper-left pane shows a list of commits (represented by yellow and blue dots)
- The lower-right pane shows which files were impacted by the commit - in this case, only blue.html
- The lower-left pane displays the full details of files which have changed in the commit. It only shows the differences - not the whole system. So in this case it only shows blue.html

Here's the commit pane in more detail:

![[Pasted image 20210610165649.png]]

- Each dot shows a separate commit in the project's history
- The yellow dot indicates where HEAD is pointing to currently - i.e. which commit you're currently using
- The green box indicates which branch that particular commit belongs to.

Dot types:
- Blue dot is a regular commit
- Yellow dot indicates the current commit - i.e. where HEAD is pointing to
- Green dot indicates changes that are staged (checked into index using git add) but not committed
- Red dot indicates local uncommitted changes, i.e. neither staged (checked into index) nor committed.

#git