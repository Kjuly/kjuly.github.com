---
layout: post
title: "Xcode Project Version Management"
date: 2012-04-28 14:36
comments: true
categories: 
- iOS
- Xcode
---

1. `Add Build Phase`(right bottom corner) -> `Add Run Script` after the `Copy Bundle Resources` phase in the target for the application. The exact insertion point in the target doesn’t matter, as long as it’s after copying the bundle resources.

2. Insert the following script ([raw](https://gist.github.com/2516617)):

        #!/bin/bash
        cd $PROJECT_DIR
        # BUILD_VERSION=`/usr/local/bin/git rev-parse --short HEAD`
        BUILD_VERSION=`git rev-parse --short HEAD`
        cd $BUILT_PRODUCTS_DIR/$PRODUCT_NAME.app
        # Note: It's Info.plist, not Proj-Info.plist
        RELEASE_VERSION=$(/usr/libexec/PlistBuddy -c "Print CFBundleShortVersionString" Info.plist)
        /usr/libexec/PlistBuddy -c "Set CFBundleVersion $BUILD_VERSION" Info.plist
        # here, 5 is my index of version part in |PreferenceSpecifiers| array
        /usr/libexec/PlistBuddy -c "Set :PreferenceSpecifiers:5:DefaultValue $RELEASE_VERSION ($BUILD_VERSION)" Settings.bundle/Root.plist

3. The script gets the build version by asking git for the short commit hash. It then gets the short release version (aka. the marketing version) from the Info.plist files and injects the build version back into the Info.plist. Note that I’m trying to mostly follow Apple’s guidelines around build and release numbers (login required).

4. __Adjust the last line to point at your Settings.bundle plist file where the version string needs to be as well as the exact index and value that you want set.__ In my case the version field is of type “Title” and sits at index 5 in the Root.plist Settings page. The DefaultValue is set to a formatted string of the release version followed by the git commit hash in parentheses.

Now every time you build the target the current git commit hash will be injected into the settings bundle as well as the Info.plist for your application.


### Reference:

- [Version numbers in iOS apps][]
- [PlistBuddy Mac OS X Manual Page][]

[Version numbers in iOS apps]: http://imadjine.tumblr.com/post/2928231079/version-numbers-in-ios-apps
[PlistBuddy Mac OS X Manual Page]: https://developer.apple.com/library/mac/#documentation/Darwin/Reference/ManPages/man8/PlistBuddy.8.html
