---
aliases: [See changes for a single line in Git history]
---

Say I want to view the history of a single line, line 71. I can do this:

	git log -u -L 71,71:script.py

It will generate the below result in this case:

	$ git log --pretty=short -u -L 71,71:script.py
	commit 1a969e3a829334c4b3b29ba41102760cdb224577
	Author: Leo King <leo.king@emailserver.com>
	
	    Some fix
	
	diff --git a/script.py b/script.py
	--- a/script.py
	+++ b/script.py
	@@ -71,1 +71,1 @@
	-print("hello world")
	+print("hollow world")
	
	commit b4902316114605ff79a2b7d8d3ba3a6f20c96e07
	Author: Leo King <leo.king@emailserver.com>
	
	    Some other fix
	
	diff --git a/script.py b/script.py
	--- /dev/null
	+++ b/script.py
	@@ -0,0 +22,1 @@
	+print("hello world")

Thus you can see which commit affected that line