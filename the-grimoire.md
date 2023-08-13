# The Grimoire
This page covers advanced concepts, and interactions between features.

## Generic functions and overloads
[Open in Playground](https://www.typescriptlang.org/play?#code/CYUwxgNghgTiAEAzArgOzAFwJYHtXygAooAueAZwxi1QHMBKMy6ugbgChRJYEV1s8BYmVTIAtgCMQMRvFGTpHLtDhI0mXPiKkKVGrXgAfOeKkymeukZMKYHdnw2CJw3SwYX3HRwPwud8maygYoO6r7w-p761iHmbjHGcfAA3uzwGfBwGMgwWhwAvuxh-JpIODgAPAAq8CAAHhggqMDkWSBQwHgQAJ7waADWqDgA7qgA2gC6AHyE9WSEAHTLsLTkZNX08AC80-AAbjhYwFsp7Tl58PWs8EWIFcT0HAD0zwB6APwODxJP7K+fIA)

Generic functions and overloads do not work well together.
When given an overloaded function as a parameter,
generics use the last overload (excluding the implementation signature).

Because of this, the last overload *should* always be a catch-all overload.

## Generics, Conditional Types, Interfaces and Lazy Evaluation

Interface definitions are not evaluated until its properties need to be checked.
This may happen if you use an indexed access type (`T["a"]`), or when checking assignability -
either in an assignment (`let a: T = {}`), or a conditional type (`T extends U ? V : W`)

<!-- stuff about how generics are lazily evaluated,
except when they contain a conditional type as the outermost type -->
