# Turing Machines

Yuxiang Lin  
CS 201  
2023-02-21

## Turing Machine

- A DFA.
- A tape (or two stacks) that holds a string of symbols.
- A tape head that can read from and write to a tape.

## Halting Problem

The halting problem is __undecidable__.

- Assume there is a function __halt(f, x)__ that can decide if __f__ will halt for input __x__.
- Create a function __g(f)__ that loops infinitely if __f(f)__ halts (which can be decided by __halt(f, f)__), and halts otherwise.
- Call __g(g)__ will than create a paradox.
- Therefore, __halt(f, x)__ does not exist.

It has the implication that many problems equivalent to it are now also undecidable, like the problem of finding whether any two programs are equivalent or not.

## Recursively Enumerable Language

Recursively enumerable languages are the languages that can be recognized by a Turing machine.

It can be described equivalently as:

1. There exists a Turing machine that can enumerate all valid strings of the language.
2. There exists a Turing machine that will accept any string in the language, but will reject or __loop forever__ when given a string not in the language.

## Pushdown Automata: Something in Between

It is a DFA with only a single stack that can recognize context-free languages. Context-free languages are described by a series of production rules (string replacement rules), each replacing a single nonterminal (a terminal symbol is a basic symbol, and the final string will only contain terminal symbols) symbol with a series of symbols, starting from a starting symbol.
