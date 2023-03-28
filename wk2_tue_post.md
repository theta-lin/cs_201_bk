# Input and Output

Yuxiang Lin  
CS 201  
2023-01-17

## Definitions

__Command-line input:__ An abstraction for providing arguments (strings) to a program.  
__Standard input stream:__ An abstraction for an infinite input sequence.  
__Standard output stream:__ An abstraction for an infinite output sequence.

## Abstraction

The theoretically infinite input and output streams allow computations that are not strictly bounded by the memory consumption of the data processed, permitting computation on a large amount of data with time being almost the only restriction.

The standardized I/O streams also allow programs to interoperate with each other seamlessly.

# Why input in Java is so painstaking?

While the standard output in Java is fairly straightforward to use, reading from the standard input requires the use of wrappers like `Scanner` around the standard input stream. I think it is for this reason that the textbook provides a library for standard input.

Java's `Scanner` is explicit in two ways: Firstly, you have to manually create a instance of `Scanner` on `System.in`, yet creating multiple `Scanner` is [usually discouraged](https://stackoverflow.com/questions/19766566/java-multiple-scanners) as they all consume the same stream and may interfere with each other in unexpected ways. Secondly, each element of the input is parsed explicitly by calling methods like `nextInt()` and `nextLine()`. Such explicitness of `Scanner` seems to encourage the user to wrap the input functionality in their own library.

[The handling of whitespaces](https://stackoverflow.com/questions/13102045/scanner-is-skipping-nextline-after-using-next-or-nextfoo) by the input methods can be problematic as `nextInt()` only consumes the integer itself and not the whitespace following it, so a call to `nextLine()` is needed to consume the newline character before reading the next line.

The explicit nature of Java's input can also be traced to its language features. Firstly, it cannot implement a C++'s `cin` style input as it does not support operator overloading. I would like to deviate a bit to discuss about `cin`. While it makes clever use of operator overloading to make the syntax for input rather clean, it can [cause problems](https://www.reddit.com/r/cpp/comments/gtzsnm/we_need_to_do_better_than_cin_for_new_programmers/) in handling erroneous inputs. Therefore, having explicit input methods can be beneficial in sanitizing the input.

The second language feature is that when passing by reference in Java, the actual values of the primitive data type wrappers like `Integer` or `Double` cannot be changed (what seems to be changing the value of `Integer` is actually creating a new `Integer` with the new value and assigning the resulting address to the variable), and `String` is immutable in a similar way. Therefore, there cannot be equivalents of C's `scanf()`, though the functionality of `scanf()` can be replaced by regular expression capture groups.
