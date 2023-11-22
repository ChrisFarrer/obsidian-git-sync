---
Title: Github_Basics
Source: https://www.youtube.com/watch?v=RGOj5yH7evk
Date: 2023-11-20
Created: 2023-11-20 09:43
Modified: 2023-11-20 09:43
tags:
---
# Git and Github Basics

What is Git?
A free and open source version control system. The most widely used version control system by developers today.

### Version Control

- Def: The management of changes to documents, computer programs, large web sites, and other collections of information.
### Terms to know

- Directory
	- i.e. Folder
- Terminal or Command Line
	 - Interface for Text Commands
- CLI
	- Command Line Interface
- cd
	- Change Directory
- Code Editor
	- Word Processor for Writing Code (like VS Code)
- Repository
	- Project, or the folder/place where your project is kept
- Github
	- A website that hosts your repositories online

### Git Commands

- clone
	- Bring a repository that is hosted somewhere like Github into a folder on your local machine
- add
	- Track your files and changes in Git
	- Can add a specific file directly, or stage all files using a period (.) or --all flag
- commit
	- Save your files in Git
	- Usually followed by the -m flag, which let's you add a description to the commit. You can also use two -m's to add a header and description body text.
		- Such as git commit -m "Bug fix at line x" -m "Corrected floating point arithmetic error."
	- git commit -am "" adds and commits at the same time, but it only works for modified files not newly created files
- push
	- Upload Git commits to a remote repo, like Github
- pull
	- Download changes from remote repo to your local machine, the opposite of push
- status
	- Shows all of the files that were updated, created, or deleted, but haven't been saved in a commit yet

### SSH Keys

In order to push changes to github, you have to prove that you own the account somehow. This can be done by generating a ssh key locally or by creating a personal access token on github. 

- For example:
	- ssh-keygen -t rsa -b 4096 -C "your_email@gmail.c0m"
- Then, specify the file you want to save your key in, and an optional passphrase
	- By default, the key will be saved under your user directory in the .ssh directory, and be called ID_RSA
- To see your keys, navigate to the repo's director and enter:
	- ls | grep testkey
- There will be two keys generated, both sharing the same name with one having a .pub extension. ONLY USE the key with the .pub extension. 
	- The .pub key is a public key. Once give Github the public key, it will compare it to your local private key, and mathematically that public key could only have been generated with your unique private key.
- To print the public key, enter:
	- cat testkey.pub
- After copying the output, navigate to Settings in github, select SSH keys, and create a new ssh key. Add a relevant title and paste the key. 
	- It will prompt you to enter your master password
- Now, you have to make sure your local Git CLI knows about the key you just generated.
	- 1) Start SSH-agent in the background
		- enter: 
			- eval "$(ssh-agent -s)"
			- Agent pid 59566
	- 2) If using macOS Sierra 10.12.2 or later, you will need to modify your ~/.ssh/config file to automatically load keys into the ssh-agent and store passphrases in your keychain.
		- enter:
			- open ~/.ssh/config
			- If it doesn't exist, touch ~/.ssh/config
		- Inside of the config file, enter:
			- Host github.com
				- AddKeysToAgent yes
				- UseKeychain yes
				- IdentifyFile ~/.ssh/key_name_or_ID
		- If you didn't use a passphrase, omit the UseKeychain line
	- 3) Finally, add the ssh key to the ssh-agent and store the passphrase in the keychain
		- enter:
			- ssh-add --apple-use-keychain ~/.ssh/key_name
	- These steps can also be found on GitHub's [official documentation]((https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent#adding-your-ssh-key-to-the-ssh-agent)

### Adding Local Repository to Github

- To initialize the repository, navigate to the directory and enter:
	- git init
- Add the files you want to be tracked:
	- git add .
- Commit the changes
	- git commit m "initial commit"
- Create an empty repository on github, then enter:
	- git remote add origin "auto-generated link to github repo"
- To check that the remote repo has been added, enter:
	- git remote -v
- Now, you can push the changes to github
	- git push origin main
- You can also set an upstream by entering:
	- git push -u origin master
	- In the future, you can just enter git push without having to specify "origin master" every time

### Github vs Local Git Workflow

![[Github_vs_Local_Workflow]]

### Git Branching

- Why is branching useful?
	- Branching allows us to create an isolated environment to develop code without directly effecting the main program. For example, a feature branch mimics the main branch, and allows us to work on and test a feature while keeping the main branch separate. 
- Each branch can't see edits or commits by other branches
- After working on a feature branch, you can merge it back to the master branch to apply your changes.


![[Git Branching Diagram.png]]
### Git Branching Terminal Commands

- git branch
	- Shows branches associated with repo, with a * next to the branch you're currently on
- git checkout -b branch_name
	- Creates a new branch and automatically switches to that branch
	- "checkout" switches branches
	- -b branch_name creates new branch
- git merge branch_name
	- merges branch_name with current branch
	- Instead merging directly, the more common professional workflow is to push the branch changes to github, then submitting a pull request (PR)
- git branch -d branch_name
	- deletes branch


### Pull Requests

After committing changes to your branch, you can generate a pull request to submit your code for review before merging with a base branch. 

Github will automatically generate a URL upon pushing changes to a branch that will allow you to submit a pull request.

After adding a title and description about what you changed, you can submit your branch for review. Github also checks for merge conflicts, essentially making sure your code doesn't break the base branch.

If your pull request is approved and your branch is merged to the base branch, typically you would delete the feature branch and switch back to the base or main branch.


### Merge Conflicts

When multiple people are working on the same code, sometimes merging branches can cause conflicts with the base branch. This can occur by either by using the "checkout" command and switching branches before committing changes, or by manually merging to the main branch.

To avoid falling behind in the main branch, you can merge the main branch to your feature branch. 


### Undoing in Git

To unstage a file, you can use:
```
git reset <file> 
```

To undo a commit, you can use:
```
git reset HEAD~1
```
- HEAD refers to the last commit
- ~1 tells git to go back 1 commit

To go back to a specific commit, you can use:
```
git log
```
to find the commit's unique hash code, then add that to the end of git reset

To both unstage and hard reset the code, you can use:
```
git reset --hard <commit_hash>
```


### Forking

Why fork a repo?

If you don't have access to a repository, you can't directly edit any of the code. Forking automatically creates a copy of a repository that you can edit. 

Once you've changed the forked code, you can even create a pull request against the original to get your changes added to the original version. 

You can also merge and create pull requests against your own version. By forking and exploring branches from larger repositories, you can get familiar with best practices and git structure. 

You can also run CRUD operations on a repository. 

## Graphics

_Insert Excalidraw Graphics Here_

## Resources & References

Helpful tools 
### LaTex References

- Summations: $\sum_{n=1} ^{\infty} a_i x^i$
- Fractions: $\dfrac{numerator}{denominator}$
- Theta: $A(n) \in \Theta(n^{\log_b a}) = \Theta(n^{\log_2 2} ) = \Theta(n)$
- Omega: $A(n) \in \Omega(n^{\log_b a}) = \Omega(n^{\log_2 2} ) = \Omega(n)$
- Big-O: $O(n^2)$  | $O(\lg{n})$

### Resources/Worksheets

_Link To Worksheet PDF_
