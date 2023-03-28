# Introduction to Theoretical CS
Yuxiang Lin  
CS 201  
2023-02-20

## Formal Language

- Alphabet: A finite set of symbols.
- Rules/Grammar: How to combine symbols from the alphabet to form a valid language.

## Regular Language

A language is __regular__ if and only if it can be specified by an regular expression (CS: An Interdisciplinary Approach, p. 725).

## Regular Expression

- Union: R | S
- Concatenation: RS
- Closure: R*
- Parentheses: \(R\)

Precedence: parentheses > closure > concatenation > union

## Kleene's Theorem

REs, DFAs, and NFAs are equivalent models, in the sense that they all characterize the regular languages (Kleene, 1951).

### NFAs and DFAs are equivalent

For a NFA of $n$ states, one can construct a DFA of $2^n$ states, each describing all the states that the NFA could possibly be in after reading some input. The transition of a state in such a DFA for an input symbol would consist of the set of possible states reached in the NFA after reading the symbol when in the original set of possible states.

### NFAs and REs are equivalent

Regular expressions can be converted to NFAs using [Thompson's construction](https://en.wikipedia.org/wiki/Thompson%27s_construction).

## Formal Languages that are not Regular

The language that includes an equal number of $0$s and $1$s cannot be described by an DFA.

- Suppose there is an DFA that can only accept this kind of language.
- Suppose that this DFA has $n$ states.
- It must recognize a string of $(n + 1)$ counts of $0$ followed by $(n + 1)$ counts of $1$.
- By reading $(n + 1)$ $0$s, it must have visited at least one state twice, as there are only $n$ states.
- Therefore, by reducing the length of the $0$ substring by the length of the substring read between the two visits to the same string, it will still arrive at the same state after reading the shorted $0$ substring.
- Thus, it would still accept the original string with some $0$s removed, invalidating the assumption that this DFA can only accept a string with an equal number of $0$s and $1$s.
