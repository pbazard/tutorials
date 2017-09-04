






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
Final methods CANNOT BE OVERRIDEN in subclasses. Useful to preserve a specific logic from modifications
in subclasses.

#### On a variable
Once defined, the value cannot be changed.
```
final int finalValue = 5;
```

#### On an argument

```
void MethodWithFinalArgument(final int finalArgument){
    finalArgument = 5; //Compilation Error
}
```
