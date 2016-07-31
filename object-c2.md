* Objective-c is a super set of C, everything works in C in also works in Objective-c.

* Static functions and static variables are only visible in current file, or they are globally visible.

* Using directive `property` to declare instance' properties, using `nonatomic` to decorate properties for single-thread application.

* Automatic Reference Counting is a technology that used by Objective-c to manage application's memory. It counts
   object's ownership, when an object has no owners, it will be destroyed by system.

* `strong` & `weak` & `copy` tell the compile what kinds of relationships objects should have.
  
  - `strong` is default attribute of object's property, it creates a relationship which is counted by ARC.
  - `weak` creates a relationship that won't be counted by ARC, object pointed by is property will be destroyed
    even it still has `weak` references. A common use case for `weak` attribute is parent-child data structure, parent
    has strong reference to children and children has weak reference to parent.
  - `copy` is an alternative of `strong` property. Instead of taking ownership of existing object, it copy that object
    when every you assign object to that propery, and take ownership of new object.

* All attributes you should now for modern iOS application.

  - getter=
  - setter=
  - readonly
  - nonatomic
  - strong
  - weak
  - copy

* .h file is the declaration of APIs that provided by the Class. And stuffs that exists in implementation file and
  aren't provided in .h file can be treated as `private`.

* Use selector to dynamically invoke method on an object. Selectors are internal representation of method name in
  Objective-C.

```
  SEL driveMethod = @selector(driveFrom:to:);
  [car performSelector:driveMethod withObject:@"Guangzhou" withObject:@"Shenzhen"];
```


