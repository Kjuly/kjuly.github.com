---
layout: post
title: "Vim Regular Expression Note"
date: 2012-02-19 14:14
comments: true
categories: 
- Vim
- Regular Expression
---

1. Copy row (`\(.*\)` -> `\1`):

        :%s/^\(.*\)\ =/\1\ =\ \1;/g

    __E.g.__:  
    (_**OT Tip**: When you mean “for example,” use `e.g`. It is an abbreviation for the Latin phrase "exempli gratia". When you mean “that is,” use `i.e.` It is an abbreviation for the Latin phrase "id est"._)  
    Original File:

        "NameLeft_1" =
        "NameLeft_2" =
        ...

    Result:

        "NameLeft_1" = "NameLeft_1"
        "NameLeft_2" = "NameLeft_2"
        ...

2. Remove blank lines:

        :%s/^$\n//g
