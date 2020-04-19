# CONFIGURING YOUR WINDOWS SYSTEM

## 1. Install command line tools

You will need to install certain tools that will be used throughout the course.

### Install Git

Git is used to track the state of your code over time. [GitHub](http://github.com/) has built its platform on Git technology. We will be using both Git and GitHub in this class to distribute code, submit assignments, and offer feedback. Git can be downloaded and installed from [this](https://git-scm.com/download/win) URL.

### Configure Git

In order to interact with Git, you'll need to first open the Git Bash utility. A quick way to access this terminal is by right clicking your desktop and choosing "Git Bash".

Copy and paste the following two commands (separately) into Git Bash. Replace the name and email address values with your own.

```
git config --global user.name "YOUR NAME"
git config --global user.email "YOUR EMAIL ADDRESS"
```
(source: [GitHub](https://help.github.com/en/github/getting-started-with-github/set-up-git))

Next, copy and paste one of the following commands into your terminal:

```
git config --global core.editor "code -w"
```

### Install Node

Refer to the package installer on Node’s [website](https://nodejs.org/en/) Select the "Recommended For Most Users" version (labeled "LTS"). Then just follow the set-up instructions.

## Configure Node

Copy and paste the following command into Git Bash, then press Enter:

```
notepad ~/.bashrc
```

The Notepad application opens, displaying a blank document.

Return to Git Bash, copy and paste the following command into Git Bash, then press Enter:

```
npm get prefix
```

Select the path value that's returned from this command, then copy it to the Clipboard (ctrl + C) to use below.

Return to the Notepad application, then within the document you opened above, do the following:

Type `export PATH="`
Paste the path you copied above from Git Bash
Type `/bin:$PATH"`

Save your changes, then close Notepad.

Continue with 2. Set up GitHub Enterprise below.

# 2. Set Up GitHub Enterprise

We will be using the GitHub Enterprise service to share some of our code. We will learn about the underlying technology of GitHub known as `git` in the next lesson.

> Note: If you already have an SSH key set up in git (for instance, for a personal or work account on github.com), use the steps in Configuring Git to use Multiple Accounts (Windows) instead of those below.

1. Log into your account at https://git.generalassemb.ly
2. Follow [these instructions](https://help.github.com/en/enterprise/2.15/user/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) to create a new SSH Key (a special, very secure, key which allows your laptop access to your github account without having to remember your github password)
3. Add your new SSH Key to GitHub Enterprise following [these instructions](https://help.github.com/en/enterprise/2.15/user/articles/adding-a-new-ssh-key-to-your-github-account)
4. Verify your key works by running the following:

```
ssh -T git@git.generalassemb.ly
```

You should see output similar to:

`Hi <you>! You've successfully authenticated, but GitHub does not provide shell access. Connection to git.generalassemb.ly closed.`

# 3. Bonus
By default, Git commands are only accessible in Git Bash. This can result in needing to switch between two different terminal programs depending on what you're doing. To make git commands available in Windows PowerShell, follow the instructions at [https://git-scm.com/book/uz/v2/Appendix-A%3A-Git-in-Other-Environments-Git-in-Powershell](https://git-scm.com/book/uz/v2/Appendix-A%3A-Git-in-Other-Environments-Git-in-Powershell).

## Helpful Debugging Tips

### Error installing due to permissions

Permissions issues are common when installing programs on the terminal. In order to install command line utilities, you need to be signed into a user account on your computer with administrator-level rights. If you have trouble with this, please ask a member of the instructional team for help.

### Google is your friend

Even experienced programmers occasionally need to look up error messages on Google. If you experience an error, it’s likely that someone else has experienced the error, as well. To find the fix, copy and paste the error message into Google, but remove content specific to your computer to ensure the accuracy of your search. You will most likely find a reference to your specific error. StackOverflow is a trustworthy reference.

### Common Issues and Fixes:

* `EACCES` error: change directory permissions to install Node and npm without the need to use sudo:

```
sudo chown -R $(whoami) /usr/local/lib/node_modules
```

* Permission denied (publickey): Use the following command to manually add the key to the keychain:

```
ssh-add -K ~/.ssh/id_rsa_ga
```

Then retry your previous command.

* Existing GitHub account that uses SSH (and existing id_rsa file): save your new key as `~/.ssh/id_rsa_ga`, and then edit the git config file as follows:

	* In your editor, open your home directory, navigate to the `.ssh` folder, then open the file named `config` (if this file doesn't exist, go to the terminal, run `touch ~/.ssh/config`, then open the file in your editor.)
	* Edit your file using the following as a template:

```
    # my GitHub account 
    Host personal
      HostName github.com
      User git
      AddKeysToAgent yes
      UseKeychain yes
      IdentityFile ~/.ssh/id_rsa
      IdentitiesOnly yes
    
    # GA github Enterprise
    Host GA   
      HostName git.generalassemb.ly
      User git
      AddKeysToAgent yes
      UseKeychain yes
      IdentityFile ~/.ssh/id_rsa_ga
      IdentitiesOnly yes
    
    # wildcard
    Host *
      AddKeysToAgent yes
      UseKeychain yes
```

* Save your changes