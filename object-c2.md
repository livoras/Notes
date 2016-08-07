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

* A protocol is a group of properties and methods that can be implemented by any class interfaces. 

```
  @protocol Runnable <NSObject>
    - (void)sayYourName:(NSString *)name;
  @end
```

* Using protocol to make type check.

```
  id <Runnable> objectCanRun = [[Car alloc] init]; // 范型?
```

Objects are of class that implemented the Runnable protocol can be assigned to variable `objectCanRun`, even they are
classes that without any relationships.

A common use case is to let you alter the behavior of certain classes without the need to subclass them.

* Category

Category is used to extend existing classed without modifying the original source code. This can avoid monolithic big
class. And you can split them into different modules, and combine the parts you need when use them. Categories are just
implemented as normal Objective-C class's .h and .m files.

Car+Maintenance.h
```
#import 'Car.h';

@interface Car (Maintenance)

- (void)saySomething;

@end

```

Car+Maintenance.m
```
#import 'Car+Maintenance.h'

@implementation Car (Maintenance)

- (void)doSomething {
  NSLog(@"Hello World");
}

@end
```

main.m
```
#import 'Car.h'
#import 'Car+Maintenance.h'
...
```

Categories can be used to implement "protected" methods, thought I don't think it's useful.

* All methods in Objective-C are public, there is no way to truly hide them from client code.

* Blocks are just like functions. But they can be dynamically created at runtime, and they are anonymous and share state
  inside the blocks that defined them, that says closures. They can be created, passed, and returned, and seems that
  they are higher-order functions in JavaScript and other functional programming languages.

```
int (^saySomethingDirty)(int, int); // declare a block variable, just like defining a funciton pointer.
saySomethingDirty = ^int(int x, inty) { // create and assign a new block to that variable
  return x + y;
};
saySomethingDirty(x, y); // call it just like normal function
```

The form of defining a block is real just like defining a function pointer, and also, you can use `typedef` to define a
new type to avoid verbose code.

```
typedef int(^SaySomethingDirty)(int, int); // now you are defining a new type

...
int main () {
  SaySomethingdDirty dirtyFunc = ^(int x, int y) {
    // return type can be omitted, if there are no parameters, (..) can be also ommited.
    return x + y;
  };
}
```

