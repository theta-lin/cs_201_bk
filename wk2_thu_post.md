# Functions

Yuxiang Lin  
CS 201  
2023-01-19

## Definition of a Java function

- Takes zero or more _input_ arguments.
- Returns zero or one _output_ value.
- May cause _side effects_.

## Abstraction

As with the mathematical functions, Java functions can be considered a mapping from the input domain to the output range, or a black box that promises to return certain outputs for certain inputs. Java functions are more general than mathematical functions in a sense that they can cause [side effects](https://en.wikipedia.org/wiki/Side_effect_(computer_science)), which allow them to modify state variable values outside its local environment. These can include outputting to the terminal or changing the states of a pseudo-random number generator.

Nevertheless, in my opinion, Java functions might not be more general than mathematical functions in the way that they must describe a concrete process of computation, instead of possibly stating that "the output would satisfy certain constraints", etc.

## Java is always pass-by-value

While it is often said that objects in Java is passed by reference, if you consider Java's parameter passing from the variable's perspective, [it is always pass-by-value](https://www.javadude.com/articles/passbyvalue.htm). The word "reference" is confusing as its original meaning (as is used in C++) is that it would serve as an alias for the variable passed by reference, so that the assignment operations upon the references are equivalent to assignment operations upon the original variables. However, in Java, references are more like pointers, assigning one reference to another is simply assigning the address of the object from one reference to another. But when accessing the member variables or functions of an object, Java would deference the object pointer before accessing the member variables or functions, so Java's `.` operator is more like C++'s `->`. Therefore, Java actually passes by value all the time, with the value being a value of a primitive type or an address to an object.

Thus, due to the pass-by-value nature of Java, it is impossible to create a function like C++'s `std::swap()` that can swap the variables referenced in the parameters. For object reference variables passed, what would be swapped would be the address contained in the parameter variables and not the actual objects. Although Java and Python shares a similar concept of "object references", swapping two variables in Java is a more painstaking process as Python provides a simple syntax for tuples that can facilitate easy swapping while Java does not, therefore requiring the use of temporary variables or bitwise operation hacks for integers.
