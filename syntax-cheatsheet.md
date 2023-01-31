# Syntax Cheatsheet

## Conventions
All types and classes will be named `T`, `U`, `V` in that order.

Everything else - e.g. variables, functions, keys and namespaces -
will be named `a`, `b`, `c` or `A`, `B`, `C`, in that order.

All functions take 0 parameters, unless the feature is related to function parameters.

All strings will use single-quotes (`''`), except when template strings (`` ` ` ``) are necessary.

If you still can't find the syntax construct, try using spaces in different places.

JavaScript constructs are here for completeness,
however they will not have their own page in the language reference.

Relevant links to the [TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/intro.html) will be in the form (HB).

Relevant links to the [Mozilla Developer Network JavaScript reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference) will be in the form (MDN).

# List of Syntax Elements
<!-- consider adding grammar productions -->
- [`a: T`](language-reference/type-annotation) - type annotations
- [`let a!: T`, `var a!: T`](language-reference/non-null-declarations) - non-null declarations
- [`a?: T`, `a(b?: T)`](language-reference/functions#optional-parameters)
- [`module A {}`](language-reference/namespaces) - namespaces
  ([HB](https://www.typescriptlang.org/docs/handbook/namespaces.html))
(soft deprecated - prefer `namespace`) (&lt;v1.0+)
- [`namespace A {}`](language-reference/namespaces) - namespaces
  ([HB](https://www.typescriptlang.org/docs/handbook/namespaces.html))
  ([v1.5+](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-1-5.html#namespace-keyword), [i2159](https://github.com/microsoft/TypeScript/issues/2159), [pr2923](https://github.com/microsoft/TypeScript/pull/2923))
- [`declare namespace A {}`](language-reference/namespace#ambient-namespace) - ambient namespace
  ([HB](https://www.typescriptlang.org/docs/handbook/namespaces.html#ambient-namespaces))
- `a in b` - `in` operator
  ([HB](https://www.typescriptlang.org/docs/handbook/2/narrowing.html#the-in-operator-narrowing))
  ([MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/in))
- [`a as T`](language-reference/type-assertion) - type assertion, `as` operator
  ([HB](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#type-assertions))
  (v????+, [i296](https://github.com/microsoft/TypeScript/issues/296), [pr3564](https://github.com/microsoft/TypeScript/pull/3564))
- [`<T> a`](language-reference/type-assertion) - type assertion (legacy)
- [`<T>()`, `<T,>()`, `function a<T>`](language-reference/functions#generic-functions) - generic function
- [`<div></div>`, `<a></a>`, `<div />`, `<a />`](language-reference/jsx) - JSX
  ([HB])
  ([MDN](https://developer.mozilla.org/en-US/docs/Learn/Tools_and_testing/Client-side_JavaScript_frameworks/React_getting_started))
  (v++++?, [i3203](https://github.com/microsoft/TypeScript/issues/3203), [pr3564](https://github.com/microsoft/TypeScript/pull/3564))
- [`type T`](language-reference/types) - type
- [`type T<U>`](language-reference/types#generic-types) - generic type
- [`class T`](language-reference/classes) - class
- [`class T<U>`](language-reference/classes#generic-classes) - generic class
- [`<const T>`](language-reference/generics#the-const-modifier) - `const` generic modifier
  (~~HB~~)
  ([v5.0+](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-5-0.html#the-const-generic-modifier), [i30680](https://github.com/microsoft/TypeScript/issues/30680), [i41114](https://github.com/microsoft/TypeScript/issues/41114), [pr51865](https://github.com/microsoft/TypeScript/pull/51865))
- [`@a`](language-reference/decorators) - decorator
  ([v1.5+](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-1-5.html#decorators))
- `#a` - JavaScript private field
  ([HB](https://www.typescriptlang.org/docs/handbook/2/classes.html#caveats))
  ([MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/Private_class_fields))
- [`this`](language-reference/interfaces#the-this-type) - `this` type
  ([HB](https://www.typescriptlang.org/docs/handbook/2/classes.html#this-types))
- [`this is T`](language-reference/type-guards#this-based-type-guards) - `this`-based type guard
  ([HB](https://www.typescriptlang.org/docs/handbook/2/classes.html#this-based-type-guards))
- [`a is T`](language-reference/type-guards#user-defined-type-guards) - user-defined type guard
- [`T extends U ? V : W`](language-reference/conditional-types) - conditional types
  ([v2.8+](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-2-8.html#conditional-types))
  ([HB](https://www.typescriptlang.org/docs/handbook/2/conditional-types.html#handbook-content))
  - recursive conditional types
    ([v4.1+](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-4-1.html#recursive-conditional-types))
  - [`T extends T ? U : never`, `T extends U ? V : never`](language-reference/conditional-types#distributive-conditional-types) - distributive conditional types
    ([v2.8+](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-2-8.html#distributive-conditional-types))
    ([HB](https://www.typescriptlang.org/docs/handbook/2/conditional-types.html#distributive-conditional-types))
- [`class T extends U`](language-reference/classes#the-extends-clause) - class/interface `extends` clause
  ([HB](https://www.typescriptlang.org/docs/handbook/2/classes.html#extends-clauses))
  ([MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/extends))
- [`class T implements U`](language-reference/classes#the-implements-clause) - class `implements` clause
  ([HB](https://www.typescriptlang.org/docs/handbook/2/classes.html#implements-clauses))
- [`interface T extends U`](language-reference/interfaces#the-extends-clause)
- [`a satisfies T`](language-reference/satisfies-operator) - `satisfies` operator ([v4.9+](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-4-9.html#the-satisfies-operator))
- [`// @ts-expect-error`](language-reference/semantic-comments#ts-expect-error) - error suppression
  ([v3.9+](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-9.html#-ts-expect-error-comments))
- [`// @ts-ignore`](language-reference/semantic-comments#ts-ignore) - diagnostic suppression
- [`// @ts-check`](language-reference/semantic-comments#ts-check) - typechecking activation
  ([HB](https://www.typescriptlang.org/docs/handbook/intro-to-js-ts.html#ts-check))
- [`// @ts-nocheck`](language-reference/semantic-comments#ts-nocheck) - typechecking suppression
  ([HB](https://www.typescriptlang.org/docs/handbook/intro-to-js-ts.html#ts-check))
- [`{ [T in keyof U]: V; }`, `{ [T in U]: V; }`](language-reference/mapped-types) - mapped type
  - also see [homogeneous mapped types](language-reference/mapped-types#homogeneous-mapped-types)
([v3.1+](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-1.html#mapped-types-on-tuples-and-arrays))
  - [`{ [T in keyof U]?: V; }`, `{ [T in U]?: V; }`, `{ [T in keyof U]-?: V; }`](language-reference/mapped-types#modifiers) - optional mapped type modifier
    ([HB](https://www.typescriptlang.org/docs/handbook/2/mapped-types.html#mapping-modifiers))
  - [`{ readonly [T in keyof U]: V; }`, `{ readonly [T in U]: V; }`, `{ -readonly [T in keyof U]: V; }`](language-reference/mapped-types#modifiers) - `readonly` mapped type modifier
    ([v3.4+](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-4.html#readonly-mapped-type-modifiers-and-readonly-arrays))
    ([HB](https://www.typescriptlang.org/docs/handbook/2/mapped-types.html#mapping-modifiers))
  - [`{ [T in keyof U as V]: W; }`, `{ [T in U as V]: W; }`](language-reference/mapped-types#key-remapping) - key remapping
    ([v4.1+](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-4-1.html#key-remapping-in-mapped-types))
    ([HB](https://www.typescriptlang.org/docs/handbook/2/mapped-types.html#key-remapping-via-as))
- [`readonly [T]`](language-reference/) - readonly tuple
  ([v3.4+](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-4.html#readonly-tuples))
- [`readonly T[]`](language-reference/) - readonly array
  ([v3.4+](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-4.html#readonly-mapped-type-modifiers-and-readonly-arrays))
- [`{ [a: string]: T; }`, `{ [a: number]: T; }`, `{ [a: T]: U; }`](language-reference/index-signatures) - index signature
- [`a as const`](language-reference/const-assertions) - `const` assertion
  ([v3.4+](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-4.html#const-assertions), [i10195](https://github.com/microsoft/TypeScript/issues/10195), [i20195](https://github.com/microsoft/TypeScript/issues/20195), [i26979](https://github.com/microsoft/TypeScript/issues/26979), [pr29510](https://github.com/microsoft/TypeScript/pull/29510))

<!-- TODO: just search through the changelogs -->
<!--
TODO
https://github.com/microsoft/TypeScript/pull/29478
-->

## Non-syntax elements
(Yes, they're technically not syntax, but they're included here for)
- return type inference
  (v3.4+, [i5487](https://github.com/microsoft/TypeScript/issues/5487), [i11152](https://github.com/microsoft/TypeScript/issues/11152), [pr29478](https://github.com/microsoft/TypeScript/pull/29478))

## Operators

- [`a!`, `a!.b`, `a![b]`, `a!()`](language-reference/nullability#non-null-assertions) - non-null assertions
  ([HB](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#non-null-assertion-operator-postfix-))
- `a?.b`, `a?.[b]`, `a?.b()` - optional chaining
  ([MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining))
- `a ?? b` - nullish coalescing
  ([MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing))

## Syntax Elements from JavaScript
- `var a` - `var` declaration
(soft deprecated - prefer `let` or `const`. note that there are differences)
  ([MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var))
- `let a` - `let` declaration
  ([v1.5+](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-1-5.html#let-and-const-support))
  ([MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let))
- `const a` - `const` declaration
  ([v1.5+](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-1-5.html#let-and-const-support))
([MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const))
- `{ [a]: b }` - computed property name
  ([v1.5+](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-1-5.html#computed-properties))
  ([MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Object_initializer#computed_property_names))
- `for (const a in b)`, `for (let a in b)`, `for (var a in b)` - `for`-`in` statement
([MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...in))
- `for (const a of b)`, `for (let a of b)`, `for (var a of b)` - `for`-`of` statement ([v1.5+](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-1-5.html#forof-support))
  ([MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of))
- `for await (const a of b)`, `for await (let a of b)`, `for await (var a of b)` - `for await`-`of` statement
  ([MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for-await...of))
- `import a from 'b';`, `import * as a from 'b';`, `import { a } from 'b';`, `import { a as b } from 'c';` - ES6 module (ESM) `import` statement
  ([HB](https://www.typescriptlang.org/docs/handbook/modules.html#import))
  ([MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import))
  (v????, [pr1983](https://github.com/microsoft/TypeScript/pull/1983))
- `export * from 'a';`, `export ` - ES6 module (ESM) `export` statement
  ([HB](https://www.typescriptlang.org/docs/handbook/modules.html#export))
  ([MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/export))
  (v????, [pr1983](https://github.com/microsoft/TypeScript/pull/1983))

<!-- remember to mention that classes are similar to interfaces-->
<!--
  consider also class#extends-clause etc.
  remember to go into the differences between class extends and interface extends
  (are there differences between class extends and interface implements?)
-->
<!--
  consider adding comprehensive docs (usage, usecases, pitfalls) for helper types
  (note that they aren't syntax)
-->