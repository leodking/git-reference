Say I have the file `comp_luna.go` on `master` branch. I was making some changes on `feature` branch, and I'm not ready to merge everything yet, but I do in fact want to grab the changes for that one file. Do this

		$ git branch
		* master
			feature

		$ git checkout -p feature comp_luna.go

This will do an **interactive checkout**, applying changes selectively as I like. If I just want to grab the whole file and don't want to make any modifications, drop the `-p` switch.