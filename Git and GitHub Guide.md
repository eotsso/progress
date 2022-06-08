# Git Commands
- Clone -> bring a repository that is hosted somewhere like Github into a folder on a local machine
- add -> track file changes in Git
- commit -> save files in Git
- push -> upload git commits to a remote repo (github)
- pull -> download changes from remote repo to local machine, (opposite of push)

# Pulling from GitHub
1. git clone `https://github.com/eotsso/progress.git 

# Viewing all Files in a Directory
- `ls -la` shows all files in a directory, even hidden ones (windows)
- `la` shows all files in a directory, even hidden ones (mac)

# Saving Changes to Git
-  `git status` shows all the files that have been changed or created
	- shows tracked and untracked files. 	
- `git add .` tracks all the files shown in `git status`
- `git add [file_name.ext]`

# Commiting a File
- `git commit -m "[TITLE message description]"`
- `git commit -m "[TITLE msg] -m "[description box]"` 

# SSH Keys (required to push files)
- Generate a ssh key locally using `ssh-keygen -t rsa -b 4096 -C "[githubemail@example.com]"`
	- Default location of key is in `/Users/wilson/.ssh/id_rsa` : 
		- The command prompt will tell you to specify the name, else saves as id_rsa
- CMD will ask to enter passphrase (can leave blank).
- Search for key generated using: `ls `
	- `testkey` //private key, DO NOT SHARE. It proves ownership of public key. 
	- `testkey.pub` //this is the one you want for public repo
- To show `testkey.pub`, enter `cat testkey.pub`, which will display ssh-rsa at start, and email at end. Copy to clipboard
- Go to GitHub --> Settings --> 