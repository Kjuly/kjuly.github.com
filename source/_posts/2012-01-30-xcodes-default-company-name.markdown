---
layout: post
title: "XCode's Default Company Name"
date: 2012-01-30 20:17
comments: true
categories: 
- Mac
- iOS
---

In terminal:

    defaults write com.apple.Xcode PBXCustomTemplateMacroDefinitions '{ORGANIZATIONNAME="TheDefaultCompanyNmaeHere";}'

`XCode` will try to pull this information from the entry in the system address book.

## References:

- [How to replace the company name in the template headers in Xcode?][]

[How to replace the company name in the template headers in Xcode?]: http://stackoverflow.com/questions/1132855/how-to-replace-the-company-name-in-the-template-headers-in-xcode
