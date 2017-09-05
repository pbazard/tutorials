


# String

## StringBuffer

## StringBuilder

## Questions
* What is the difference between StringBuffer and StringBuilder in Java?




## Modifiers
Access modifiers:
* Private
* Public
* protected
* default

Non access modifiers
* final
* static

### Default modifier
Nothing in fromt of it (class, method, variable). 
Accessible from inside the package only.
That's why Default access is also called Package access. 
    
```
class DefaultAccessClass {
    ...
}
```
Same package + subclasses in the SAME package.

### Private access
Used on variables and methods. NOT ALLOWED on class.
This example is not valid:
```
private class DefaultAccessClass {
    // NOT VALID MODIFIER
}
```
private variables and methods are accessible only in the class where 
they are defined
Private methods and attributes from the superclass NOT accessible in the subclasses.

### Protected
Same package + Available to subclasses in ANY package.

### Public
Accessible everywhere.

### Final
#### On a class
cannot be EXTENDED (subclassed). Necessary for IMMUTABLE classes because we 
don't want to break immutability with subclassing. String class is used in 
hashcode calculation for example, so might result in security issues.
Examples:
```
public final class String {
    ...
}
```
or wrapper classes:
```
public final class Integer {
    ...
}
```

#### On a method
CANNOT BE OVERRIDEN

### Static
This keyword can be used to create static variables, methods or classes. Java 5
also introduced static imports which allows to import static members of one class
into aonther one and allowing to use them like they are member of this class.

There is only one copy of the static variable in the heap which can be accessed
and altered by any object.

Static variables or methods are initialized when the class is loaded in the JVM.
On the other hand, instance members are created either by using the `new()` operator 
or using reflection like `Class.newInstance()`. That's wy you cannot access
a non-static variable from a static context: those variables are not yet created
at compile time.

* Can you access a non-static variable (instance variable) in a static context?
```
public class StaticTest {
    private int count = 0;
    public static void main(String[] args){
        count++; // COMPILER ERROR: non-static variable cannot...
    }
}
```

