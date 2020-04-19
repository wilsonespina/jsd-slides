# CONFIGURING YOUR LINUX SYSTEM

## 1. Install command line tools

You will need to install certain tools that will be used throughout the course.

### Install Git

Git is a tool used to track the state of your code over time. [GitHub](https://github.com/) is a company that has made a business on top of the Git technology. We will be using both Git and GitHub in this class to distribute code, submit assignments and offer feedback.

Git can be installed by running the following command:

```
sudo apt-get install build-essential git-core curl
```

### Configure Git

Copy and paste the following two commands (separately) into your terminal. Replace the name and email address values with your own.

```
git config --global user.name "YOUR NAME"
git config --global user.email "YOUR EMAIL ADDRESS"
```
(source: [GitHub](https://help.github.com/en/github/getting-started-with-github/set-up-git))

Next, copy and paste one of the following commands into your terminal:

```
git config --global core.editor "code -w"
```

### Install Node.js

```
curl --silent --location https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install --yes nodejs
apt-get install --yes build-essential
```

When you’re done, add a thumbs up emoji 👍 to the post on Slack. Then complete the instructions in the section 2. Setting up GitHub below.

## 2. Set Up GitHub Enterprise

We will be using the GitHub Enterprise service to share some of our code. We will learn about the underlying technology of GitHub known as `git` in the next lesson.

* Log into your account at [https://git.generalassemb.ly](https://git.generalassemb.ly)
* Follow [these instructions](https://help.github.com/en/enterprise/2.14/user/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) to create a new SSH Key (a special, very secure, key which allows your laptop access to your github account without having to remember your github password)
* Add your new SSH Key to GitHub Enterprise following these instructions
* Verify your key works by running the following:

```
ssh -T git@git.generalassemb.ly
```

You should see output similar to:

`Hi <you>! You've successfully authenticated, but GitHub does not provide shell access. Connection to git.generalassemb.ly closed.`

## Helpful Debugging Tips

### Error installing due to permissions

Permissions issues are common when installing programs on the terminal. In order to install command line utilities, you need to be signed into a user account on your computer with administrator-level rights. If you have trouble with this, please ask a member of the instructional team for help.

### Google is your friend

Even experienced programmers occasionally need to look up error messages on Google. If you experience an error, it’s likely that someone else has experienced the error, as well. To find the fix, copy and paste the error message into Google, but remove content specific to your computer to ensure the accuracy of your search. You will most likely find a reference to your specific error. StackOverflow is a trustworthy reference.

### Common Issues and Fixes:

We recommend the following remedies to issues that commonly arise during the installation of command line utilities:

* Mac users may run into the problem of an outdated version of Git installed with Xcode being given precedence in the terminal. If you experience this issue, you’ll need to adjust your shell path by following the instructions under "Trumping Xcode's Older Git" in this article.

* Mac users running OS 10.11 or later may need to [disable the System Integrity Protection](https://osxdaily.com/2015/10/05/disable-rootless-system-integrity-protection-mac-os-x/) on their machine before installing certain command line utilities.

* Students experiencing an `EACCES` error should change directory permissions to install Node and npm without the need to use sudo: 

```
sudo chown -R $(whoami) /usr/local/lib/node_modules
```

* Students with Homebrew installed on their machines should run `brew update` in order to get the latest version of Homebrew.

* Students who need to update their installations of npm can run `npm install -g npm`.

* Students with an existing, outdated installation of Node can update their install by following the directions above (i.e., using the package installer).

* Students experiencing a Permission denied (publickey) error with GitHub Enterprise should following the troubleshooting steps at https://help.github.com/enterprise/2.14/user/articles/error-permission-denied-publickey/.

* Students with an existing GitHub account that uses SSH should edit the git config file as follows:

	* In your editor, open your home directory, navigate to the `.ssh` folder, then open the file named `config` (if this file doesn't exist, go to the terminal, run `touch ~/.ssh/config`, then open the file in your editor.)
	* Add a second entry to your file using the following as a template (note that everything after a # is a comment):

```	
  # my GitHub account
  Host personal
    HostName github.com
    User git
    AddKeysToAgent yes
    UseKeychain yes
    IdentityFile ~/.ssh/id_rsa

  # GA GitHub Enterprise
  Host GA   
    HostName git.generalassemb.ly
    User git
    AddKeysToAgent yes
    UseKeychain yes
    IdentityFile ~/.ssh/id_rsa_ga # this should match the filename you used when saving your new key
```

* Save your changes