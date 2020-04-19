# CONFIGURING GIT TO USE MULTIPLE ACCOUNTS (MAC)

If you use multiple accounts with Git (for instance, a work or personal GitHub account in addition to your GA GitHub Enterprise account), you need to configure git a bit differently than the default instructions outlined on github.com. Use this page as your guide for finishing your GitHub Enterprise setup.

* Log into your account at [https://git.generalassemb.ly](https://git.generalassemb.ly)
* Follow these steps to create a new SSH Key (a special, very secure, key which allows your laptop access to your github account without having to remember your github password).

### Generating a new SSH key

* Open Terminal.
* Paste the text below, substituting in your GitHub Enterprise email address.

```
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```
This creates a new ssh key, using the provided email as a label.

* When you're prompted to "Enter a file in which to save the key," type
```
/Users/[username]/.ssh/id_rsa_ga
```

where `[username]` is your Mac username, and then press **Enter**.

* At the prompt, type a secure passphrase. For more information, see ["Working with SSH key passphrases"](https://help.github.com/en/enterprise/2.15/user/articles/working-with-ssh-key-passphrases).

### Adding your SSH key to the ssh-agent

* Paste the text below to start the ssh-agent in the background.

```
eval "$(ssh-agent -s)"
```

The output should be `Agent pid` followed by some numbers.

* In your editor, open your home directory, navigate to the `.ssh` folder, then open the file named `config` (if this file doesn't exist, go to the terminal, run `touch ~/.ssh/config`, then open the file in your editor.)
Add a second entry to your file using the following as a template:

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
* Paste the text below to add your SSH private key to the ssh-agent and store your passphrase in the keychain. (If you used a name other than id_rsa_ga in the steps above, be sure to use that name here as well.)

```
ssh-add -K ~/.ssh/id_rsa_ga
```

* Add your new SSH Key to GitHub Enterprise following [these instructions](https://help.github.com/en/enterprise/2.15/user/articles/adding-a-new-ssh-key-to-your-github-account)
Verify your key works by running the following:
ssh -T git@git.generalassemb.ly

You should see output similar to:

`Hi <you>! You've successfully authenticated, but GitHub does not provide shell access. Connection to git.generalassemb.ly closed.`