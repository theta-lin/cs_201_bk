# Abstract Data Type

Yuxiang Lin  
CS 201  
2023-02-07

## Which Object methods to override?

Reference: https://stackoverflow.com/questions/44274406/when-should-i-be-overriding-java-lang-object-methods

`clone()`

Implement to get a copy of the object, but was to some degree implemented poorly and has some caveats. Therefore, its use was [discouraged by some people](https://www.artima.com/articles/josh-bloch-on-design#part13). But this might be the only way to create a copy of the object when the object is referenced by its parent class.

`equals()`

Implement to compare two objects for equality. Required for the object to be used as key in `HashMap`, or inserted into `HashSet`.

`hashCode()`

Required for the object to be used as key in `HashMap`, or inserted into `HashSet`.

`toString()`

Allows the conversion of the object into String when needed.

`finalize()`

Never, as there is no guarantee for it to be called for cleanup.

## Interface

Defined in the [official documentation](https://docs.oracle.com/javase/tutorial/java/IandI/createinterface.html):

> In the Java programming language, an interface is a reference type, similar to a class, that can contain only constants, method signatures, default methods, static methods, and nested types. Method bodies exist only for default methods and static methods. Interfaces cannot be instantiated—they can only be implemented by classes or extended by other interfaces.

Default methods and static methods are added in Java 8.

For default methods, you can now implement methods in interfaces, but this [reintroduced some problems that multiple inheritance might incur](https://www.javacodemonk.com/diamond-problem-of-inheritance-in-java-8-88faf6c9) (though nowhere as severe as in C++).

For static methods, there was actually [no good reason for them not be implemented earlier](https://stackoverflow.com/questions/512877/why-cant-i-define-a-static-method-in-a-java-interface) (before Java 8).

You cannot have protected methods in interfaces, and private methods are only there because they could be used by other default methods in the interface. [The rationale for this is possibly mainly because "interface" literally means what you can see from the outside](https://stackoverflow.com/questions/5376970/protected-in-interfaces).

Constants in interfaces mean __public static final__, which removes the possibility to have protected constants to be used only internally.
