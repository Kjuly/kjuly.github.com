---
layout: post
title: "MVC in Cocoa"
date: 2012-02-16 11:06
comments: true
categories: 
- iOS
- Cocoa
---

#### Combining Roles

One can merge the MVC roles played by an object, making an object, for example, fulfill both the controller and view roles—in which case, it would be called a view controller. In the same way, you can also have model-controller objects. For some applications, combining roles like this is an acceptable design.

A `model controller` is a controller that concerns itself mostly with the model layer. It “owns” the model; its primary responsibilities are to manage the model and communicate with view objects. Action methods that apply to the model as a whole are typically implemented in a model controller. The document architecture provides a number of these methods for you; for example, an NSDocument object (which is a central part of the document architecture) automatically handles action methods related to saving files.

A `view controller` is a controller that concerns itself mostly with the view layer. It “owns” the interface (the views); its primary responsibilities are to manage the interface and communicate with the model. Action methods concerned with data displayed in a view are typically implemented in a view controller. An NSWindowController object (also part of the document architecture) is an example of a view controller.


#### Design Guidelines for MVC Applications

...

- Although you can combine MVC roles in an object, the best overall strategy is to keep the separation between roles. This separation enhances the reusability of objects and the extensibility of the program they're used in. If you are going to merge MVC roles in a class, pick a predominant role for that class and then (for maintenance purposes) __use categories in the same implementation file to extend the class to play other roles__.

...

- ...Specific recommendations vary by the MVC roles of the two classes involved:

    * A view class shouldn't depend on a model class (although this may be unavoidable with some custom views).
    * A view class shouldn't have to depend on a mediating controller class.
    * A model class shouldn't depend on anything other than other model classes.
    * A mediating controller class shouldn’t depend on a model class (although, like views, this may be necessary if it's a custom controller class).
    * A mediating controller class shouldn't depend on view classes or on coordinating controller classes.
    * A coordinating controller class depends on classes of all MVC role types.


### Reference:

- [Cocoa Design Patterns][]

[Cocoa Design Patterns]: https://developer.apple.com/library/ios/#documentation/Cocoa/Conceptual/CocoaFundamentals/CocoaDesignPatterns/CocoaDesignPatterns.html
