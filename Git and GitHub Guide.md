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
- Go to GitHub --> Settings --> SSH and GPG keys, and paste the key inside. 
## Adding your SSH key to the ssh-agent 
- Type `eval "$(ssh-agent -s)"` , which will return `Agent pid ####`
- If on MAC, modify `~/.ssh/config ` by adding the following command:
```shell
Host *
	AddKeysToAgent yes
	UseKeychain yes
	IdentityFile ~/.ssh/id_rsa 
```
- Add SSH private key to ssh-agent by typing the following. If you created a key with a ***different*** name, replace id_rsa from the following phrase
	- `$ ssh-add ~/.ssh/id_rsa` (FOIR WINDOWS)
	- `ssh-add -K ~/.ssh/id_rsa`  (FOR MAC)
		- *If error, ensure that the file path is correct.*
- Now SSH keys are set up. 
# Push
- `git push origin master ` 
	- pushes everything to the master branch

# Pushing Locally to GitHub
- Navitgate to .git file path in the terminal (use `cd`)
-  `git init` --> makes a git repo in the *current* file path. 
- `git status` --> checks all untracked and tracked files.
- `git add .` or `git add [file name.ext]` --> adds the file to be tracked by git. 
- `git commit -m "message"` --> commits/saves the changes to git, must include 1 message (or 2)

### Push to live now
- `git push origin master` this won't work because there's no connected repo. 
- First, create an empty repo on GitHub. Copy the SSH key. 
- `git remote add origin [SSH key]`
- now `git push origin master` will work.  

# Sources
https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent
