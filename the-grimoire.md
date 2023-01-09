# The Grimoire
This page covers advanced concepts, and interactions between features.

## Generic functions and overloads
Generic functions and overloads do not play well.
When given an overloaded function as a parameter,
generics tend to use the last overload (the implementation signature).

Note that if you are writing typings for a JavaScript library,
the typings may not have an implementation signature,
meaning generics may use an unexpected overload.

## Generics, Conditional Types, Interfaces and Lazy Evaluation
stuff about how interfaces are lazily expanded,
and generics too, except when they contain a conditional type as the outermost type
