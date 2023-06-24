**git log** - is used to print information about git commits. It may look something like this:

	$ git log
	commit 6357c8d60adc49d0f5270072abc3019e80dff126 (HEAD -> master)
	Author: Leo King <leo.king@emailserver.com>
	Date:   Mon Jun 7 17:09:19 2021 +0100

    First commit - Create index page
	
The long string "6357c8d60adc49d0f5270072abc3019e80dff126" is a **[[SHA-1]]**

- git log --oneline <- compress logs onto one line for easy reading
- git log --oneline foo.txt <- get only logs which show the history of foo.txt

#git