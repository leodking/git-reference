	[alias]
			graph = log --graph \\  
					   --abbrev-commit \\  
					   --decorate \\  
					   --date=relative \\  
					   --format=format:'%C(bold blue)%h%C(reset) - %C(bold red)(%ar)%C(reset) %C(white)%s%C(reset) %C(dim white)- %an%C(reset)%C(bold magenta)%d%C(reset)' \\  
					   --all
					   
You can put the above text in your gitk (there should already be an `[alias]` section). Then it will produce pretty outputs