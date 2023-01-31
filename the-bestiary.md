# The Bestiary

This page contains various helper types and useful constructs.

Note that in general, needing advanced types like these
are an indication that you're trying to get TypeScript to do too much.

## `AnyT`

```ts
interface MyGeneric<T> { foo: T; }
type AnyMyGeneric = MyGeneric<unknown>;
type MyConditional<T extends string | number> = T extends string ? 'string' | 'number';
type AnyMyConditional = MyConditional<any>;
interface MyInvariantGeneric<T> { foo: T; bar(t: T): void; }
type AnyMyInvariantGeneric = MyInvariantGeneric<any>;
```

This is a type `AnyMyGeneric` that's defined so that any `MyGeneric<T>` extends it.  
Usually this can be done by making the generic parameter default to `unknown`:

```ts
interface MyGeneric<T = unknown> {
  foo: T;
}
```

But it may be useful to seperate it out for a number of reasons:

- You want to make sure the user explicitly specifies the type
- The default would be very unsafe (e.g. `any`)

## Constrained identity function

```ts

```

## Type maps

```ts
type TypeMap = {
  foo: Foo;
  bar: Bar;
};
```

TODO: show use cases

## `NoInfer<T>`

[Open in Playground](https://www.typescriptlang.org/play?#code/C4TwDgpgBAcg9gSQHYDMICcA8AVAfFAXigG1sBdUqCAD2AiQBMBnKAVyQGsk4B3JKAPxQADFABcUJBABuGMgG4gA)

```ts
type NoInfer<T> = [T][T extends unknown ? 0 : never];
```

This type prevents TypeScript from using that location to infer `T` in a generic.

[Open in Playground](https://www.typescriptlang.org/play?#code/C4TwDgpgBAcg9gSQHYDMICcA8AVAfFAXigG1sBdUqCAD2AiQBMBnKAVyQGsk4B3JKAPxQADFABcUJBABuGMgG4AUIoYQAxgBsAhumgp2a4AEs4-BolQYACjq0BbHLgAU1CdgCUbpas069B41NJCzR0G3R7RxcJeGRQx08obCU1UyZgKGoARgkAIzg4DQgtfiJzOOtbOycs9xS0jOoAJjyCopLCYIqwqpq6xVSkdMyAZk7ubvD7PqUAelmoRagAPQFlH21dKH0kQxMzEIwAeVyAK3VgKNcoAG8oLS8oXMeAX0TklXVN-13A-gnLOgTudDFcJHcHrBDlg8PInq93vUho0ACydcqA4EXJwQiQAciyeIANPCoE0oG85gslqsBg1MgBWcbQrGGHH3fGEknPMkU-rzJYrARAA)

```ts
declare function doInferParam<T>(x: T): T;
declare function noInferParam<T>(x: NoInfer<T>): T;
const x1: boolean = doInferParam(1);
//    ^^ error here - T is `number`
const x2: boolean = noInferParam(1);
//   error here - T is `boolean` ^
const x3 = noInferParam(1);
//    ^? - const x3: unknown
// Note that this doesn't error because TypeScript defaults
// any parameter it can't infer to `unknown`, which typechecks fine in this case.

declare function doInferObject<T>(x: { a: T; b: T }): T;
declare function noInferObject<T>(x: { a: NoInfer<T>; b: T }): T;
const x4 = doInferObject({ a: "1", b: 2 });
//    ^? - const x4: string        ^ type error here, `T` is inferred from `a`
const x5 = noInferObject({ a: "1", b: 2 });
//    ^? - const x5: number
//                         ^ type error here, `T` is inferred from `b`
```

## `UnionToIntersection<T>`

(by [@jcalz](https://github.com/jcalz): [SO](https://stackoverflow.com/questions/50374908/transform-union-type-to-intersection-type/50375286#50375286))
[Open in Playground](https://www.typescriptlang.org/play?#code/C4TwDgpgBAqgdgSwPZwCpIJJ2BATgZwgGNhk4AeGAPigF4oAKGKCADxzgBN9YoB+RgFcAXLACUdGgAYoouBABueCWw7dGCUQjgAzPFAwTa0-lACi7XAEMS5DABpYNOYrwBuIA)

```ts
type UnionToIntersection<U> = (U extends U ? (u: U) => 0 : never) extends (
  i: infer I
) => 0
  ? Extract<I, U>
  : never;
```

This type converts unions (`T | U | V`) into intersections (`T & U & V`).

## `IsEqual<T, U>`

(by [@mattmccutchen](https://github.com/mattmccutchen): [ic27024](https://github.com/microsoft/TypeScript/issues/27024#issuecomment-421529650))
[Open in Playground](https://www.typescriptlang.org/play?#code/C4TwDgpgBAkgzgUQI4FcCGAbAPAFQDRQCqAfFALxQAUWAasZQJTmk1QQAewEAdgCZxQcUAPxQAjFABcUAAxMOXPgOp1GzKKwU9+REeKmymo4ACcU0aQDNMcCAG4gA)

```ts
type IsEqual<T, U> = (<V>() => V extends T ? 1 : 0) extends <V>() => V extends U
  ? 1
  : 0
  ? true
  : false;
```

This type checks equality of types using the compiler's notion of equality. Some differences between this, and types that `extends` each other, are shown below.

[Open in Playground](https://www.typescriptlang.org/play?#code/C4TwDgpgBAkgzgUQI4FcCGAbAPAFQDRQCqAfFALxQAUWAasZQJTmk1QQAewEAdgCZxQcUAPxQAjFABcUAAxMOXPgOp1GzKKwU9+REeKmymo4ACcU0aQDNMcCAG4AUKEiw4AWRTBPmDCACCcHAAlgDm3GgARhgQuAQk5FAA2vhEALpsnNoCiYQEOOnGZhZQ1hi2js7QAMIA9gC2YGgmMSnxFInwyOjYrcQE8B5ewD7+gaHhUS1xxKmODjwodVAIUADeUGgJMgQRCRIAvk7g0DgSFLUNTTHbssSOAPT3UM8AesJHLjgATAkXjc1YdZoaQyOxQfZQABkaygEWkYjB+wIQJBYLh4kRdwcj2eUDeHxOAGZfvV-jE0NwQMiNqjwVica93pVBAAWEmXAEIAgyKAAH3E9KejIJggArOyyVhKJRgbI+eImGRSHIoVQZfD5V9FcqGNT1XL+WIGLT9RJ+VraftBbj8cycAA2CVXKWyuCmILcELaqAANxqQV4BH1bpMHq96hQ3AA1twagB3bjWxlAA)

```ts
type IsMututallyAssignable<T, U> = [T, U] extends [U, T] ? true : false;
type Compare<T, U> = [IsEqual<T, U>, IsMututallyAssignable<T, U>];

enum E {
  a = 0,
  b = 1,
}
type T1 = Compare<0, 0>;
//   ^? - type T1 = [true, true]
type T2 = Compare<{ a: 0 } & { b: 1 }, { a: 0; b: 1 }>;
//   ^? - type T2 = [false, true]
type T3 = Compare<any, { a: 0 }>;
//   ^? - type T3 = [false, true]
type T4 = Compare<E, 0 | 1>;
//   ^? - type T4 = [false, true]
type T5 = Compare<
  ((a: 0 | 1) => 0) & ((a: 1 | 2) => 0),
  { (a: 0 | 1): 0; (a: 1 | 2): 0 }
>;
//   ^? - type T5 = [false, true]
type T6 = Compare<(a: string) => void, (a: string) => unknown>;
//   ^? - type T6 = [false, true]
```

## `Narrow<T>`

(by [@tjjfvi](https://github.com/tjjfvi))
[Open in Playground](https://www.typescriptlang.org/play?#code/C4TwDgpgBA+gcgQwE5IPYHcA8AVANFAVQD4oBeKAbQIF0oIAPYCAOwBMBnS7WgfkKgBcUAKKMkCAMbAc+YgG4AUKEhREKDDjJQArswDWzDMxKkFAH1hq0WPFAAMUC820BbAEYQkUAGRQA3gC+ROaWyNYy9syOUG4AlgDmsczAPv5BIfBhGrYARDnR7MBISfGpgcEWmeo2+G6oqAA2EAjGGVbZ+Owg7o0VodURFNR9VeG2fpQwQgAKaJBIoADSECDUQu3oUOkWABTYdIwsHFCobgBWEFJQfBMUi1BJUHorqABmUNzrWTZ3w1uCUGYEAAbp4AJQhURFSTSQLRZwNBrRXSsCCvJIQVj4bBEORAA)

```ts
type _Narrow<T, U> = [U] extends [T] ? U : Extract<T, U>;
type Narrow<T = unknown> =
  | _Narrow<T, 0 | (number & {})>
  | _Narrow<T, 0n | (bigint & {})>
  | _Narrow<T, "" | (string & {})>
  | _Narrow<T, boolean>
  | _Narrow<T, symbol>
  | _Narrow<T, []>
  | _Narrow<T, { [_: PropertyKey]: Narrow }>
  | (T extends object ? { [K in keyof T]: Narrow<T[K]> } : never)
  | Extract<{} | null | undefined, T>;
```

This type is used to narrow the type of an expression to as exact of a type as possible.
It can be used either as a generic constraint, or in a `satisfies` clause.

[Open in Playground](https://www.typescriptlang.org/play?#code/C4TwDgpgBA+gcgQwE5IPYHcA8AVANFAVQD4oBeKAbQIF0oIAPYCAOwBMBnS7WgfkKgBcUAKKMkCAMbAc+YgG4AUKEhREKDDjJQArswDWzDMxKkFAH1hq0WPFAAMUC820BbAEYQkUAGRQA3gC+ROaWyNYy9syOUG4AlgDmsczAPv5BIfBhGrYARDnR7MBISfGpgcEWmeo2+G6oqAA2EAjGGVbZ+Owg7o0VodURFNR9VeG2fpQwQgAKaJBIoADSECDUQu3oUOkWABTYdIwsHFCobgBWEFJQfBMUi1BJUHorqABmUNzrWTZ3w1uCUGYEAAbp4AJQhURFSTSQLRZwNBrRXSsCCvJIQVj4bBERRKcDQbAARi0zncniGimUhIATFoJq96kJCsVmPFashmUUSlsqQSPgBmelQRmoLms+JDDlIIQAJUuqCQrEwLJK+DJHiQRA5AC8hHVGs0ogE8U0UuwHOQJgghETakIitoIPgJEIAOSitzIN34VhCa1CGn2yh2qBuhA+-xQG1QEkBWgBf7sBDAWLsdEQTgbRQAehzUCgAD0eAozVB2CTyBRQ0GoAL8AAWWjJ1Pp2KZ1TfHBE3EKPMF4uliDmulWkVMsMR6XutxupMptMZrNd7A03v9oslsvsIVj0VCCjhyNu2f4N0SN3UadRmOhtyBl1CIUBXVCV4IBrsaCJluL9vLgZsAFdd803BQFAkVBmEKQFvi0GQiB2MEyBITACAOJg2AAsYiEQ+ghAIZDSBIehFEg6CUmYb4gPg9CGEw44NhwYC8IIoiSNNYcRUtWDqiQnYA1jYNHWdKBXTDT1vV9f1owfGID1DI98EEuMEy2MFc1Awcy1eSteLGHt+OrfBa3rKAmw0vstK3LjXlHfTsjXfiGQnJSYk5MNZ3UzSBxslJXl3Bz0CAgTxzFSg3JPY8LyvdyZRvW1g1rcTn1fEUPy-byrN88DUQkBpkGgciYPwnR9EMdBmE480Gy0ehywXNsO2zbKwJ02ryCoviwR2ehLI3QcFCAA)

```ts
type T1 = number[];
type T2 = { foo: string, bar: string };
type T3 = { foo: string[], bar: Record<string, number>, baz: boolean };

let s0 = { a: 1, b: true, c: 'foobar', d: { a: 2, b: [1, 'a', { a: 1 }] } } satisfies Narrow;
//  ^? - let s0: { a: 1, b: true, c: "foobar", d: { a: 2, b: [1, "a", { a: 1 }] } }
let s1 = [1, 2, 3, 4] satisfies Narrow<T1>;
//  ^? - let s1: [1, 2, 3, 4]
let s2 = { foo: 'a', bar: 'b' } satisfies Narrow<T2>;
//  ^? - let s2: { foo: "a", bar: "b" }
let s3 = { foo: ['a', 'b', 'c'], bar: { a: 1, b: 2, c: 3 }, baz: false } satisfies Narrow<T3>;
//  ^? - let s3: { foo: ["a", "b", "c"], bar: { a: 1, b: 2, c: 3 }, baz: false }

const narrow = <T,>() => <U extends Narrow<T>>(x: U) => x;
const narrowT3 = <U extends Narrow<T3>>(x: U) => x;

let f0 = narrow()({ a: 1, b: true, c: 'foobar', d: { a: 2, b: [1, 'a', { a: 1 }] } });
//  ^? - let f0: { a: 1, b: true, c: "foobar", d: { a: 2, b: [1, "a", { a: 1 }] } }
let f1 = narrow<T1>()([1, 2, 3, 4]);
//  ^? - let f1: [1, 2, 3, 4]
let f2 = narrow<T2>()({ foo: 'a', bar: 'b' });
//  ^? - let f2: { foo: "a", bar: "b" }
let f3 = narrowT3({ foo: ['a', 'b', 'c'], bar: { a: 1, b: 2, c: 3 }, baz: false });
//  ^? - let f3: { foo: ["a", "b", "c"], bar: { a: 1, b: 2, c: 3 }, baz: false }

declare const x: unknown;

let s4 = x satisfies Narrow
//  ^? - let s4: unknown
let f4 = narrow()(x)
//  ^? - let f4: unknown
```
