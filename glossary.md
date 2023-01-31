# Glossary
This lists all terms related to TypeScript, common and uncommon.

See also the [Mozilla Developer Network glossary](https://developer.mozilla.org/en-US/docs/Glossary) for terms related to JavaScript and the web.

## TypeScript-specific terms
- assignable - `T` being assignable to `U` means that all possible values of the type `T` are valid values for the type `U`
- distributive conditional types - passing each member of a union through a conditional type individually, when the union is a bare type parameter (like `K`): `K extends K ? T<K> : never` turns `A | B | C` into `T<A> | T<B> | T<C>`
	([HB](https://www.typescriptlang.org/docs/handbook/2/conditional-types.html#distributive-conditional-types))
- homomorphic mapped types - mapped types acting on certain types (e.g. arrays, tuples and primitives) will return the same kind of type (arrays/tuples/primitives)

## Other computer science terms
- structural typing, structurally typed - subtyping based on the shape of types - `{ a: number; }` extends `{ a: number | string; }`, `{ a: 1; }` extends `{ a: number; }`. TypeScript's type system is structural
	([WP](https://en.wikipedia.org/wiki/Structural_type_system))
- nominal typing, nominally typed - subtyping based on explicit declarations: `class T extends U {}`.
	TypeScript doesn't have this whatsoever
	([WP](https://en.wikipedia.org/wiki/Nominal_type_system))
- f-bounded polymorphism, f-bounded quantification (`this` types) - the `this` type will take the type of child classes
	([WP](https://en.wikipedia.org/wiki/Bounded_quantification#F-bounded_quantification))
- lambda function, anonymous function - a function not bound to a name. In JavaScript, arrow function expressions and function expressions are anonymous functions
	([WP](https://en.wikipedia.org/wiki/Anonymous_function))
- closure - a function that captures ("closes over") variables from the scope it is in:
```ts
function returnsClosure() {
	let i = 0;
	return () => { i += 1; return i; };
	// this closure captures `i`, and so `i` must live at least as long as this function
}
```

## TypeScript constructs
- mapped types - types that create an object by iterating over the keys of an object type (`{ [K in keyof T]: Foo<T, K>; }`)
	([HB](https://www.typescriptlang.org/docs/handbook/2/mapped-types.html#handbook-content))
- mapped types with key remapping - mapped types that rename keys (``{ [K in keyof T as `get${K}`]: () => T[K]; }``)
- conditional types - types that resolve to one of two types based on whether `T` extends `U`: `T extends U ? V<U> : V<T>`
	([HB](https://www.typescriptlang.org/docs/handbook/2/conditional-types.html#handbook-content))

## Terms from JavaScript
- nullish coalescing - the `??` operator that returns its right operand
	if its left operand is `null` or `undefined`
	([MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing))
- optional chaining - the `?.` operator that accesses the property
	if its left operand is neiter `null` nor `undefined`
	([MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining))
- arrow function expression - `const f = () => {};`
	([MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions))
- function expression, anonymous function - `const f = function () {}`, `const f = function foo() {}`
	([MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/function))
- immediately invoked function expression (IIFE) - a function that is called right after it is defined: `(() => {})()`, `(function () {})()`
	([MDN](https://developer.mozilla.org/en-US/docs/Glossary/IIFE))