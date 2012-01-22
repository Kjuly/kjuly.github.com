---
layout: post
title: "Github Multiple Accounts &amp; SSHs"
date: 2012-01-19 18:16
comments: true
categories: 
- HowTo
- Git
---

## STEPS

1. Create the SSH key pair for another account (related post: [github:help - Set Up Git](http://help.github.com/mac-set-up-git/)).

        cd ~/.ssh  
        ssh-keygen -t rsa -C "user@example.com"

    __Note__: It'll let you enter the file path(like `/Users/Kjuly/.ssh/example_rsa`) to save it as `example_rsa`, enter the `passphrase`.  

        open -a MacVim example_rsa

    Copy it to `github` -> `Account Settings` -> `SSH Public Keys`.  
    Test whether it works:

        ssh -T git@github.com

2. Config the multiple SSH keys (related post: [Github:ors:help - Multiple SSH keys](http://ufz.github.com/help/multiple-ssh-keys/)).

        ssh-add ~/.ssh/example_rsa
        vim ~/.ssh/config

    Set it like this:

        # Default GitHub account
        Host github.com
        HostName github.com
        User git
        IdentityFile /Users/Kjuly/.ssh/id_rsa

        # Another Github account
        Host github-another
        HostName github.com
        User git
        IdentityFile /Users/Kjuly/.ssh/example_rsa

    Save the file and change the mod:

        chmod 600 ~/.ssh/config

3. Using the second key.

    You need use

        git clone git@github-another:anotherAccount/repo.git

    instead of

        git clone git@github.com:defaultAccount/my_repo.git

## ISSUES
### Q:
    Bad owner or permissions on /Users/username/.ssh/config
### A:
    chmod 600 ~/.ssh/config

## REFERENCES

- [Github:ors:help - Multiple SSH keys](http://ufz.github.com/help/multiple-ssh-keys/)
- [Multiple GitHub Accounts & SSH Config](http://stackoverflow.com/questions/3225862/multiple-github-accounts-ssh-config)
- [http://help.github.com/ssh-issues/](http://help.github.com/ssh-issues/)
- [多个github帐号的SSH key切换](http://4simple.github.com/docs/multipleSSHkeys/)
- [github:help - Set Up Git](http://help.github.com/mac-set-up-git/)
