---
layout: post
title: "Add Cocos2D to UIKit Based Project"
date: 2012-02-26 00:22
comments: true
categories: 
- iOS
- Cocos2D
---

__Q:__ When copied (or use `submodule`) all `Cocos2D lib` to current iOS projcet, building the preject will cause hundreds of errors.

__A:__  

1. Cocos2D has its lib dependences, add `framwork`s:

    - OpenGLES.framework
    - OpenAL.framework
    - AVFoundation.framework
    - AudioToolbox.framework
    - QuartzCore.framework
    - (maybe need more...)

2. When meet the error `Undefined symbols for architecture` like:

        "_inflateInit2_", referenced from:
        _inflateMemoryWithHint in ZipUtils.o
        "_inflate", referenced from:
        _inflateMemoryWithHint in ZipUtils.o
        "_inflateEnd", referenced from:
        _inflateMemoryWithHint in ZipUtils.o
        "_gzopen", referenced from:
        _ccInflateGZipFile in ZipUtils.o

    Just go to `build setting` and add `-lz` for other linking flags:

    __Detail:__ Select `Project Target` -> `Build Setting` -> search `other`, and there'll be a `Linking` tab which includes `OTHER_LDFLAGS`, add `-lz` to the target.  
    __Tip:__ Create a new Cocos2D based project, and check the setting.

