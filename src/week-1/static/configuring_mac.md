# CONFIGURING YOUR MAC SYSTEM

## 1. Install command line tools

### Install command line tools
You will need to install certain tools that will be used throughout the course.

### Configure your text editor

**Visual Studio Code**

Start Visual Studio Code (`Applications > Visual Studio Code`).

Press `shift` + `command` + `P` to open the Command Palette.

Type `shell command`, then in the displayed list, click **Shell Command: Install 'code' command in PATH.**

TODO:  ADD LINTING RULES

Close Visual Studio Code.

### Install brew

Brew is a package manager that we use to install various command line applications to your computer.

Open your terminal (`Applications` > `Utilities` > `Terminal`), paste the following command, and hit enter:

```CLI
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

### Install Git

Git is used to track the state of your code over time. [GitHub](https://github.com/) has built its platform on Git technology. We will be using both Git and GitHub to distribute code, submit assignments, and offer feedback. Use the following command to install Git:

```
brew install git
```

### Configure Git

Copy and paste the following two commands (separately) into your terminal. Replace the name and email address values with your own.

```
git config --global user.name "YOUR NAME"
git config --global user.email "YOUR EMAIL ADDRESS"
```

(source: [GitHub](https://help.github.com/en/github/getting-started-with-github/set-up-git))

Next, copy and paste the following commands into your terminal:

```
git config --global core.editor "code -w"
```

### Install Node

Refer to the package installer on Node’s [website](https://nodejs.org/en/). Select the "Recommended For Most Users" version (labelled "LTS"). Then just follow the set-up instructions.

### Ensure NPM is updated

Node has a handy package manager, which we will using frequently. It comes with Node, but NPM is updated more frequently; you will always need to have the most up-to-date version.

```
npm install npm -g
```

If you receive an error message titled `EACCES`, enter the following command to change directory permissions to install Node and npm without the need to use sudo:

```
sudo chown -R $(whoami) /usr/local/lib/node_modules
```

Then repeat the previous command, which should finish without an error.

After successfully completing the above steps, continue with 2. Set up GitHub Enterprise below.

## 2. Set Up GitHub Enterprise

We will be using the GitHub Enterprise service to share some of our code. We will learn about the underlying technology of GitHub known as `git` in the next lesson.

> Note: If you already have an SSH key set up in git (for instance, for a personal or work account on github.com), use the steps in [Configuring Git to use Multiple Accounts (Mac)]() instead of those below.

1. Log into your account at https://git.generalassemb.ly
2. Follow [these instructions](https://help.github.com/en/enterprise/2.15/user/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) to create a new SSH Key (a special, very secure, key which allows your laptop access to your github account without having to remember your github password)
3. Add your new SSH Key to GitHub Enterprise following [these instructions](https://help.github.com/en/enterprise/2.15/user/articles/adding-a-new-ssh-key-to-your-github-account
4. Verify your key works by running the following:

```
ssh -T git@git.generalassemb.ly
```

You should see output similar to:

`Hi <you>! You've successfully authenticated, but GitHub does not provide shell access. Connection to git.generalassemb.ly closed.`

### Helpful Debugging Tips

## Error installing due to permissions

Permissions issues are common when installing programs on the terminal. In order to install command line utilities, you need to be signed into a user account on your computer with administrator-level rights. If you have trouble with this, please ask a member of the instructional team for help.

## Google is your friend

Even experienced programmers occasionally need to look up error messages on Google. If you experience an error, it’s likely that someone else has experienced the error, as well. To find the fix, copy and paste the error message into Google, but remove content specific to your computer to ensure the accuracy of your search. You will most likely find a reference to your specific error. StackOverflow is a trustworthy reference.

## Common Issues and Fixes:

* Permission error when installing Homebrew: download a Git installer at [https://git-scm.com/downloads](https://git-scm.com/downloads) and use it to install Git

* `EACCES` error: change directory permissions to install Node and npm without the need to use sudo:

```
sudo chown -R $(whoami) /usr/local/lib/node_modules
```

* `Permission denied (publickey)`: Use the following command to manually add the key to the keychain:

```
ssh-add -K ~/.ssh/id_rsa_ga
```

Then retry your previous command.

* Existing GitHub account that uses SSH (and existing id_rsa file): save your new key as `~/.ssh/id_rsa_ga`, and then edit the git `config` file as follows:
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