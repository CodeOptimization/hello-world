# Sharing resources

## improperly accessing resources

1. Atomic operations like assigning or returning a boolean variable won't be interrupted.

2. Not all one line code is atomic, for example a++, which involved the plus one and assigning steps. For example:
```java
int getInteger(){
  return i++;
}
```
if _getInteger()_ is accessed by multiple threads, some threads will get an "incorrect" state, in the midst of self increment.

## Resolving shared resource contentiion

3. Preventing this kind of collision is simple a matter of putting a lock on a resource when one task is using it. It's called _serialize 
access to shared resources_. This means that at one time, there will be only one task at a time is allowed to access the resource.

4. Adding clause around a piece of code that only allows one task at a time to pass through that piece of code, which enables _mutual 
exclusion_, a common name for such a machanism called _mutex_.

5. To prevent collisions over resources, java has a built-in support int the form of the __synchronized__ keyword. When a task whiches to
 execute a piece of code guarded by the __synchronized__ keyword, it checks to see if the lock is available, the acquires it, executes the 
 code and release it.
 
6. To control access to the shared resource, you first put it inside an object. Then any method that uses the resource can be made 
__synchronized__.

7. If a task is in a call to one of the __synchronized__ methods, all other tasks are bolcked from _entering_ any of the __synchronized__ 
methods of that object until the first task returns from its call.

8. All object contain a single lock. When you call any __synchronized__ method, that  object is locked and no other __synchronized__ 
method of _that_ object can be called until the first one finishes and releases the lock. There is a single lock shared by all the 
__synchronized__ methods of a paticular object.

9. One tricky part is, you must make fields __private__ when dealing with concurrency, since the fields can be directly accessed if they 
are not __private__.

10. One task can get an object's lock multiple times and the JVM keeps track of the number of times that object has been locked by 
increasing or decreasing the counter. When the object is unlocked, the count should be zero.

11. There is also a single lock _per class_ (as part of the __Class__ object for the class), so that __synchronized static__ methods can 
lock each other out from simultaneous access of __static__ data on a class-wide basis.

12. When should you use sycnchronize? Here is _Brian's Rule of Synchronization： If you are waiting a variable tht might nextbe raed by 
another thread, or reading a variable that might have last see writen by another thraed, you must use synchronization, and further, both 
are reader and the writer mush synchronize using the same monitor lock._
