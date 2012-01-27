---
layout: post
title: "Property Memeory Management"
date: 2012-01-27 18:51
comments: true
categories: 
- iOS
---

1:

    _iVar = [[SomeClass alloc] init];

2:

    SomeClass * tempVar = [[SomeClass alloc] init];
    self.iVar = tempVar;
    [tempVar release];

3:

    // Still not sure whether this is correct.
    [self.iVar = [[SomeClass alloc] init] release];

4: Using ARC (It's turned on by default in XCode4.2)

    self.iVar = [[SomeClass alloc] init];

### REFERENCES:

- [Acceptable ways to release a property][]
- [Objective C: Proper way to init an NSArray that is a @property][]
- [Best way to set a retained property to a newly created object][]

[Acceptable ways to release a property]: http://stackoverflow.com/questions/7577453/acceptable-ways-to-release-a-property
[Objective C: Proper way to init an NSArray that is a @property]: http://stackoverflow.com/questions/5588693/objective-c-proper-way-to-init-an-nsarray-that-is-a-property
[Best way to set a retained property to a newly created object]: http://stackoverflow.com/questions/7842641/best-way-to-set-a-retained-property-to-a-newly-created-object
