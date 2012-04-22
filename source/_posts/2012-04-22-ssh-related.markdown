---
layout: post
title: "SSH related"
date: 2012-04-22 12:10
comments: true
categories: 
- SSH
- Server
- Cmd
---

Download key `foo.pem`

    $ mv foo.pem ~/.ssh/
    $ cd ~/.ssh
    $ chmod 600 foo.pem

Connect to server:

    $ ssh -D 9999 -i ~/.ssh/foo.pem ubuntu@xxx.xxx.xxx.xxx

Tip: use

    $ ssh-add foo.pem

so you can drop the `-i` option.

There's a `-v` option, that can output the debug information

---
## rsync

File transfer.

    rsync [OPTION] … SRC [SRC] … [USER@]HOST:DEST
    rsync [OPTION] … [USER@]HOST:SRC [DEST]

e.g.

    rsync -avz src/ ubuntu@xxx.xxx.xxx.xxx:destination/

options: -a 

### Reference:

- [rsync man page][]

[rsync man page]:http://ss64.com/bash/rsync.html
